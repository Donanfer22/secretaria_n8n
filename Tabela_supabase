CREATE TABLE n8n_historico_mensagens (
  id           BIGSERIAL PRIMARY KEY,
  session_id   VARCHAR(40) NOT NULL,
  message      JSONB NOT NULL,
  created_at   TIMESTAMP WITHOUT TIME ZONE NOT NULL DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_n8n_historico_mensagens_session_id ON n8n_historico_mensagens (session_id);

CREATE TABLE n8n_fila_mensagens (
  id           BIGSERIAL PRIMARY KEY,
  id_mensagem  VARCHAR(40) NOT NULL,
  telefone     VARCHAR(40) NOT NULL,
  mensagem     TEXT NOT NULL,
  "timestamp"  TIMESTAMP WITHOUT TIME ZONE NOT NULL
);

CREATE INDEX idx_n8n_fila_mensagens_telefone ON n8n_fila_mensagens (telefone);
