# Global NPM Directory

> This stops the need for doing sudo npm install's

1. Make a directory for global installations:

```bash
mkdir ~/.npm-global
```

2. Configure npm to use the new directory path:

```bash
npm config set prefix '~/.npm-global'
```

3. Open or create a `~/.zshrc` file and add this line:

```bash
export PATH=~/.npm-global/bin:$PATH
```

4. Back on the command line, update your system variables:

```bash
source ~/.zshrc
```

