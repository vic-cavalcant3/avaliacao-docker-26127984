# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome: Victor Rodrigues Cavalcante Rocha      
Matrícula: 26127984
Usuário do GitHub: vic-cavalcant3
Usuário do Docker Hub: viccavalcante

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Usei a imagem nginx:1.27-alpine como base, porque é a oficial do Nginx e a versão alpine é mais leve. No docker images, a imagem do portal ficou com 73.6MB.

2. O Nginx procura os arquivos em /usr/share/nginx/html. Para conferir, rodei o container e usei docker exec teste-portal ls /usr/share/nginx/html. Apareceram o index.html e o estilo.css, além do 50x.html, que já vem na imagem do Nginx.


## Parte 2 · Docker Hub

3. A imagem publicada é viccavalcante/agrovale-portal:1.0-26127984, e o link do repositório é https://hub.docker.com/r/viccavalcante/agrovale-portal

4. O token é mais seguro do que a senha. Ele pode ter permissão limitada (só leitura e escrita nos repositórios, por exemplo) e dá para apagar ou revogar a qualquer momento sem trocar a senha da conta. Como o computador do laboratório é compartilhado, se o login ficar salvo nele, quem usar a máquina depois não tem acesso à minha senha, só ao token, e eu posso cancelar ele depois.

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar
   a porta? Mostre o comando.

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou,
   e por quê?

10. Código de conclusão impresso pelo verificador:

```
(cole aqui)
```
