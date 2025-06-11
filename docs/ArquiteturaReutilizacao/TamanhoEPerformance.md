# 4.1.10. Tamanho e Performance

Esta seção apresenta estimativas de armazenamento, tráfego e desempenho para a plataforma de eventos, com base na estrutura do banco de dados fornecida. O objetivo é garantir um sistema escalável e com boa experiência para o usuário.

## Estimativas de Tamanho do Banco de Dados

### Tabela: usuario

**Colunas:**

- pkusuario (BIGINT): `8 bytes`
- nome (VARCHAR(100)): `~100 bytes`
- email (VARCHAR(255)): `~255 bytes`
- senha (VARCHAR(128)): `~128 bytes`
- foto_perfil (VARCHAR(255)): `~255 bytes`
- data_cadastro (DATE): `3 bytes`
- organizador (BOOLEAN): `1 byte`

**Tamanho total estimado por linha (usuário): ~750 bytes**

---

### Tabela: evento

**Colunas:**

- pkevento (BIGINT): `8 bytes`
- dataevento (DATE): `3 bytes`
- horaevento (TIME): `3 bytes`
- localevento (VARCHAR(100)): `~100 bytes`
- descricaoevento (VARCHAR(500)): `~500 bytes`
- contato (VARCHAR(100)): `~100 bytes`
- link_inscricao (VARCHAR(255)): `~255 bytes`
- possui_certificado (BOOLEAN): `1 byte`
- limite_vagas (INT): `4 bytes`
- fkcategoria (BIGINT): `8 bytes`

**Tamanho total estimado por linha (evento): ~982 bytes**

---

### Tabela: categoria

**Colunas:**

- pkcategoria (BIGINT): `8 bytes`
- categoria (VARCHAR(50)): `~50 bytes`

**Tamanho total estimado por linha: ~58 bytes**

---

### Tabela: midia_evento

**Colunas:**

- pkmidia (BIGINT): `8 bytes`
- fkevento (BIGINT): `8 bytes`
- tipo (VARCHAR(20)): `~20 bytes`
- url_arquivo (VARCHAR(255)): `~255 bytes`
- descricao (VARCHAR(200)): `~200 bytes`

**Tamanho total estimado por linha: ~491 bytes**

---

### Tabela: rel_evento_tag

**Colunas:**

- fkevento (BIGINT): `8 bytes`
- fktag (BIGINT): `8 bytes`

**Tamanho estimado por linha: 16 bytes**

---

### Tabela: rel_seguir_evento / rel_seguir_organizador

**Colunas:**

- fkusuario (BIGINT): `8 bytes`
- fkevento ou fkorganizador (BIGINT): `8 bytes`

**Tamanho estimado por linha: 16 bytes**

---

### Tabela: rel_organizador_evento

**Colunas:**

- fkorganizador (BIGINT): `8 bytes`
- fkevento (BIGINT): `8 bytes`
- data_criacao (DATE): `3 bytes`

**Tamanho estimado por linha: 19 bytes**

---

### Tabela: rel_inscricao_evento

**Colunas:**

- fkusuario (BIGINT): `8 bytes`
- fkevento (BIGINT): `8 bytes`
- data_inscricao (DATE): `3 bytes`
- status (VARCHAR(20)): `~20 bytes`
- codigo_inscricao (VARCHAR(20)): `~20 bytes`

**Tamanho estimado por linha: ~59 bytes**

---

### Tabela: rel_avaliacao

**Colunas:**

- fkusuario (BIGINT): `8 bytes`
- fkevento (BIGINT): `8 bytes`
- avaliacao (FLOAT): `4 bytes`
- comentario (VARCHAR(255)): `~255 bytes`

**Tamanho estimado por linha: ~275 bytes**

---

### Tabela: rel_favoritado

**Colunas:**

- fkusuario (BIGINT): `8 bytes`
- fkevento (BIGINT): `8 bytes`
- favoritado (BOOLEAN): `1 byte`

**Tamanho estimado por linha: 17 bytes**

---

### Tabela: rel_forum_evento

**Colunas:**

- fkevento (BIGINT): `8 bytes`
- fkusuario (BIGINT): `8 bytes`
- mensagem (VARCHAR(500)): `~500 bytes`
- data_postagem (DATETIME): `8 bytes`

**Tamanho estimado por linha: ~524 bytes**

---

### Tabela: rel_certificado

**Colunas:**

- fkevento (BIGINT): `8 bytes`
- fkusuario (BIGINT): `8 bytes`
- data_emissao (DATE): `3 bytes`
- url_pdf (VARCHAR(255)): `~255 bytes`

**Tamanho estimado por linha: ~274 bytes**

---

### Tabela: notificacao / rel_notificacao_usuario

**Colunas notificacao:**

- pknotificacao (BIGINT): `8 bytes`
- titulo (VARCHAR(100)): `~100 bytes`
- mensagem (VARCHAR(500)): `~500 bytes`

**Tamanho estimado: ~608 bytes**

**Colunas rel_notificacao_usuario:**

- fkusuario (BIGINT): `8 bytes`
- fknotificacao (BIGINT): `8 bytes`
- data_envio (DATETIME): `8 bytes`
- lida (BOOLEAN): `1 byte`

**Tamanho estimado: ~25 bytes**

---

## Estimativa do Tráfego de Rede

### Cenário Simplificado

- 2 acessos/dia
- Página inicial: 1 MB
- 2 requisições (eventos, favoritos, etc.): 200 KB cada
- Notificações ou perfil: 100 KB

**Tráfego por dia:** `1 + 0.4 + 0.1 = 1.5 MB`  
**Por mês:** `1.5 MB * 30 = 45 MB por usuário`  
**1.000 usuários:** `45 GB/mês`

---

### Cenário Mais Realista

- 3 acessos/dia
- +500 KB de upload (comentários, inscrições)

**Tráfego por dia:** `3 * 1.5 MB + 0.5 MB = 5 MB`  
**Por mês:** `5 * 30 = 150 MB por usuário`  
**1.000 usuários:** `150 GB/mês`

---

## Metas de Desempenho

| Requisição                  | Tempo de Resposta Máximo       |
|----------------------------|-------------------------------|
| Criação/edição de evento   | < 2 segundos                  |
| Recuperar detalhes de evento | < 1 segundo                  |
| Pesquisa de eventos        | < 2 segundos                  |
| Entrega de notificações    | < 5 segundos                  |
| Suporte a usuários simultâneos | 10.000 usuários           |

---

## Estratégia de Escalabilidade

- **Banco de Dados (MySQL):** Implantação em VPS com expansão conforme demanda.
- **Aplicação:** Implantada na Heroku, com suporte a escalonamento automático.
- **Cache:** Utilização de cache no navegador e na VPS.
- **Balanceamento de Carga:** Gerenciado via Nginx.


# Histórico de Versões

| Versão | Data | Descrição | Autor | Revisor | Comentário do Revisor |
| -- | -- | -- | -- | -- | -- |
| `1.0`  | 10/06/2025  | Criação do Documento Inicial| [Thales Euflauzino](https://github.com/thaleseuflauzino) e [](https://github.com/thaleseuflauzino) |  |  |