O pacote openh264 na versão **2.4** apresentou uma falha de segurança que foi prontamente corrigida, porém nos repositórios do Fedora mantidos pela Cisco o mesmo não foi atualizado rapidamente, ficando meses sem atualização.

## Remoção do pacote
Remover o pacote diretamente com `dnf remove` pode resultar na remoção de outros pacotes co-dependentes, portanto o ideal é utilizar o `dnf swap` e desabilitar o repositório Fedora Cisco.

Para remover o pacote corretamente, execute:
```sh
sudo dnf swap *\openh264* noopenh264 --allowerasing
```

Certifique-se de desabilitar o repositório Fedora Cisco, pois o sistema pode tentar "atualizar" este pacote reinstalando ele. Para isso edite o arquivo `/etc/yum.repos.d/fedora-cisco-openh264.repo` mudando as linhas que contêm `enabled=1` para `enabled=0`, verifique se o repositório foi desabilitado corretamente:
```sh
dnf repolist --all | grep openh264
```

Deve listar os repositórios com a flag `disabled`.

---

## Referências
- ChatGPT
- [Github - openh264 CVE CVE-2025-27091](https://github.com/cisco/openh264/security/advisories/GHSA-m99q-5j7x-7m9x)
- [Pagure - 12617](https://pagure.io/releng/issue/12617)
- [Fedora mail lists - remove openh264?](https://lists.fedoraproject.org/archives/list/devel@lists.fedoraproject.org/thread/MU3IKREOMSVS6RRAJEV7EGQKTHLCFYKH/)
