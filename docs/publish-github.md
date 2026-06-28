# Publicacao no GitHub

Quando a autenticacao do `gh` estiver valida, publicar este repositorio com:

```bash
cd /home/e5x401/ecommerce-diagramas
gh auth refresh -h github.com
gh repo create ecommerce-diagramas --public --source=. --remote=origin --push
```

Se o nome `ecommerce-diagramas` ja estiver em uso, troque por outro nome equivalente e atualize o comando.

Depois da publicacao, convide os colegas pelo GitHub quando for o momento de colaborar diretamente no repo.
