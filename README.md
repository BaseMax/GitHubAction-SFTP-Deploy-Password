# GitHub Actions: SFTP Deploy with Password

Automatically deploy and upload new pushed files to a server by **SFTP** protocol directly with password without SSH keys.

#### Why this one and GitHub Actions?

It took me several hours to prepare and test this configuration, I'm happy to share this for free to save others time.

GitHub Actions are great to use in projects. Happy coding ^_^

### GitHub Action

Create `.github/workflows/deploy.yml` file:

```
on: [push]

jobs:
  mirror_with_sftp:
    name: deploy
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: FTP Deployer
        uses: sand4rt/ftp-deployer@v1.4
        with:
          sftp: true
          host: ${{ secrets.SERVER_HOST }}
          port: 22
          username: ${{ secrets.SERVER_USERNAME }}
          password: ${{ secrets.SERVER_PASSWORD }}
          remote_folder: ${{ secrets.SERVER_PATH }}
          local_folder: '.'
          cleanup: false
          include: '[ "*", "**/*" ]'
          exclude: '["node_modules/**", "_secret.php", ".github/**", ".git/**", "*.env"]'
          pasive: true
```

### Variables

- `SERVER_HOST`
- `SERVER_USERNAME`
- `SERVER_PASSWORD`
- `SERVER_PATH`
