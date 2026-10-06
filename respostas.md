# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome: Victor Rodrigues Cavalcante Rocha      
Matrícula: 26127984
Usuário do GitHub: vic-cavalcant3
Usuário do Docker Hub: viccavalcante

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal (saída de `docker images`)?


 Usei a imagem nginx:1.27-alpine como base, porque é a oficial do Nginx e a versão alpine é mais leve. No docker images, a imagem do portal ficou com 73.6MB.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para conferir que o `index.html` está lá dentro.
 

O Nginx procura os arquivos em /usr/share/nginx/html. Para conferir, rodei o container e usei docker exec teste-portal ls /usr/share/nginx/html. Apareceram o index.html e o estilo.css, além do 50x.html, que já vem na imagem do Nginx.


## Parte 2 · Docker Hub

3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

 A imagem publicada é viccavalcante/agrovale-portal:1.0-26127984, e o link do repositório é https://hub.docker.com/r/viccavalcante/agrovale-portal

4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

O token é mais seguro do que a senha. Ele pode ter permissão limitada (só leitura e escrita nos repositórios, por exemplo) e dá para apagar ou revogar a qualquer momento sem trocar a senha da conta. Como o computador do laboratório é compartilhado, se o login ficar salvo nele, quem usar a máquina depois não tem acesso à minha senha, só ao token, e eu posso cancelar ele depois.

## Parte 3 · Página de manutenção

5. Preencha uma linha por defeito encontrado. Defeito inexistente listado aqui desconta pontos.

| # | Instrução | O que estava errado | O que você viu acontecer | Como corrigiu |
|---|---|---|---|---|
| 1 | COPY (faltando) | O Dockerfile não copiava a pasta `site/` para dentro da imagem | O container subiu normal, mas em localhost:7084 apareceu "Welcome to nginx!" em vez da página de manutenção | Adicionei `COPY site/ .` |

| 2 | WORKDIR | Apontava para `/usr/share/nginx`, mas o Nginx serve os arquivos de `/usr/share/nginx/html` | Com o COPY usando `.`, o arquivo ia parar na pasta errada | Troquei para `WORKDIR /usr/share/nginx/html` |



6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

O formato é `-p porta_do_host:porta_do_container`. No `-p 7042:80` eu acesso pela porta 7042 do meu PC e ela vai pra porta 80 do container, onde o Nginx está rodando, então funciona. No `-p 80:7042` eu acessaria pela porta 80 do PC, mas ia cair na 7042 do container, onde não tem nada escutando, então a página não abre. A porta do container é sempre o número da direita.

## Parte 4 · docker-compose.yml

7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

Porque cada serviço roda no seu próprio container. Se eu colocar `localhost`, o WordPress vai procurar o banco dentro do próprio container dele, e lá não tem banco nenhum. Como os dois estão na mesma rede do compose, o Docker resolve o nome do serviço `db` para o IP do container do banco, então o WordPress acha o MariaDB pelo nome.

8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar a porta? Mostre o comando.

Porque só o WordPress precisa falar com o banco, e ele faz isso pela rede interna do compose. Publicar a 3306 deixaria o banco exposto pra fora sem necessidade, o que é um risco de segurança. No `docker compose ps` dá pra ver que o `db` aparece só com `3306/tcp`, sem `0.0.0.0`. Pra consultar o banco eu entro direto no container:

docker compose exec db mariadb -u agrovale -p agrovale_blog

Ele pede a senha do `.env` e abre o terminal do MariaDB.

## Parte 5 · Persistência

9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou, e por quê?

Usei `docker compose down` pra derrubar e `docker compose up -d` pra subir de novo. O `down` remove os containers e a rede, mas mantém os volumes nomeados, então o banco e os arquivos do WordPress continuaram lá e o post sobreviveu. O comando que teria apagado o post é `docker compose down -v`, porque o `-v` remove também os volumes, e o post fica salvo no volume do banco (`/var/lib/mysql`).

10. Código de conclusão impresso pelo verificador:

AGROVALE-26127984-AFE66331