
## Padronização de mensagens
```sh
git commit -m "feat: Add search button"
```
> funcionalidade nova

```sh
git commit -m "fix: remove wrong condition on query"
```
> correção ou ajuste

```sh
git commit -m "refactor: improve code performance"
```
> refatoração de código

```sh
git commit -m "test: add tests on search results"
```
> alterações ou inclusão de testes

```sh
git commit -m "style: change Footer height"
```
> alterações nos estilos/layout

```sh
git commit -m "docs: add changelog for 2.0 version"
```
> alterações/inclusão de documentação

```sh
git commit -m "chore: change eslint rules"
```
> alterações/inclusões no ambiente de desenvolvimento

```sh
git commit -m "build: add new lib for image render"
```
> alterações de dependências

```sh
git commit -m "revert: back to 123abc commit"
```
> reversão de commit

## Comandos uteis
### Desfazer último commit (antes de ir para origin)
```sh
git reset --soft HEAD~1
```