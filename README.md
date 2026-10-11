# helix

Конфиг редактора [Helix](https://helix-editor.com), заточенный под DevOps:
Go/Rust + YAML (K8s-схемы через schemastore), Terraform/HCL, Dockerfile,
Bash (shellcheck/shfmt), JSON, TOML, Markdown.

Синхронизируется между macOS и Fedora. Живёт в `~/dev/skitalex/helix` —
`skitalex` — общая папка под разные репозитории (не репо сама по себе),
`helix/` — этот репозиторий внутри неё.

### Установка на новой машине

```bash
git clone <url-этого-репо> ~/dev/skitalex/helix
rm -rf ~/.config/helix
ln -s ~/dev/skitalex/helix ~/.config/helix
```

Проверить, что конфиг подхватился и чего не хватает из LSP:

```bash
hx --health
```

### Бинари языковых серверов

Общее через `npm` (нужно на обеих машинах одинаково):

```bash
npm i -g yaml-language-server \
         dockerfile-language-server-nodejs \
         bash-language-server \
         vscode-langservers-extracted \
         @ansible/ansible-language-server
```

#### macOS (brew)

```bash
brew install marksman shellcheck shfmt
brew install hashicorp/tap/terraform-ls
cargo install taplo-cli --locked --features lsp
```

#### Fedora (dnf / cargo)

```bash
sudo dnf install -y shellcheck
# marksman, shfmt, terraform-ls — проще через готовые бинари с GitHub releases
# или через go install / cargo install:
go install github.com/mvdan/sh/v3/cmd/shfmt@latest
cargo install taplo-cli --locked --features lsp
# terraform-ls: https://github.com/hashicorp/terraform-ls/releases
# marksman: https://github.com/artempyanykh/marksman/releases
```

### Обновление конфига

Правим файлы прямо в `~/dev/skitalex/helix/` (это и есть `~/.config/helix`,
через симлинк), коммитим и пушим как обычный git-репозиторий. На втором
компьютере — `git pull`.

Другие репозитории кладём рядом, в `~/dev/skitalex/<repo>` — у каждого
свой `.git`, друг на друга не влияют.
