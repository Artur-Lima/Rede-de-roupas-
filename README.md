# Rede-de-roupas-
Modelagem de Banco de Dados com PostgreSQL - Atividade Prática Passo a Passo
Aplicativo social de moda onde:
Pessoas organizam seu guarda-roupa;
Criam combinações (outfits);
Postam fotos conceituais;
Marcam poses;
Vendem e trocam roupas;
Negociam dentro da plataforma;
Recebem reações.

erDiagram

    PESSOA {
        uuid id PK
        varchar cpf
        varchar nome
        varchar email
        varchar senha_hash
        varchar tipo_usuario
        timestamp criado_em
    }

    LOJA {
        uuid id PK
        varchar nome
        text descricao
        uuid pessoa_id FK
        timestamp criado_em
    }

    PRODUTO {
        uuid id PK
        varchar nome
        text descricao
        numeric preco
        boolean disponivel
        uuid loja_id FK
        uuid dono_id FK
        timestamp criado_em
    }

    GUARDA_ROUPA {
        uuid id PK
        uuid pessoa_id FK
        varchar nome
    }

    ITEM_GUARDA_ROUPA {
        uuid id PK
        uuid guarda_roupa_id FK
        uuid produto_id FK
        date adicionado_em
    }

    OUTFIT {
        uuid id PK
        uuid pessoa_id FK
        varchar nome
        text descricao
        timestamp criado_em
    }

    ITEM_OUTFIT {
        uuid id PK
        uuid outfit_id FK
        uuid produto_id FK
    }

    POST {
        uuid id PK
        uuid pessoa_id FK
        uuid outfit_id FK
        text legenda
        timestamp criado_em
    }

    FOTO {
        uuid id PK
        uuid post_id FK
        varchar url_imagem
        boolean conceitual
        varchar estilo
    }

    POSE {
        uuid id PK
        varchar nome
        text descricao
        varchar referencia
    }

    FOTO_POSE {
        uuid id PK
        uuid foto_id FK
        uuid pose_id FK
    }

    REACAO {
        uuid id PK
        uuid pessoa_id FK
        uuid post_id FK
        varchar tipo
        timestamp criado_em
    }

    COMENTARIO {
        uuid id PK
        uuid pessoa_id FK
        uuid post_id FK
        text conteudo
        timestamp criado_em
    }

    CARRINHO {
        uuid id PK
        uuid pessoa_id FK
        timestamp criado_em
    }

    ITEM_CARRINHO {
        uuid id PK
        uuid carrinho_id FK
        uuid produto_id FK
        int quantidade
    }

    PEDIDO {
        uuid id PK
        uuid pessoa_id FK
        numeric valor_total
        varchar status
        timestamp criado_em
    }

    ITEM_PEDIDO {
        uuid id PK
        uuid pedido_id FK
        uuid produto_id FK
        numeric preco_unitario
        int quantidade
    }

    NEGOCIACAO {
        uuid id PK
        uuid comprador_id FK
        uuid vendedor_id FK
        uuid produto_id FK
        varchar status
        timestamp iniciado_em
    }

    TROCA {
        uuid id PK
        uuid pessoa1_id FK
        uuid pessoa2_id FK
        uuid produto1_id FK
        uuid produto2_id FK
        varchar status
        timestamp criada_em
    }

    PESSOA ||--o{ LOJA : possui
    LOJA ||--o{ PRODUTO : vende
    PESSOA ||--o{ PRODUTO : possui
    PESSOA ||--o{ GUARDA_ROUPA : organiza
    GUARDA_ROUPA ||--o{ ITEM_GUARDA_ROUPA : contem
    PRODUTO ||--o{ ITEM_GUARDA_ROUPA : pertence
    PESSOA ||--o{ OUTFIT : cria
    OUTFIT ||--o{ ITEM_OUTFIT : contem
    PRODUTO ||--o{ ITEM_OUTFIT : usado_em
    PESSOA ||--o{ POST : publica
    POST ||--o{ FOTO : possui
    FOTO ||--o{ FOTO_POSE : referencia
    POSE ||--o{ FOTO_POSE : classifica
    POST ||--o{ REACAO : recebe
    POST ||--o{ COMENTARIO : recebe
    PESSOA ||--o{ REACAO : faz
    PESSOA ||--o{ COMENTARIO : escreve
    PESSOA ||--o{ CARRINHO : possui
    CARRINHO ||--o{ ITEM_CARRINHO : contem
    PESSOA ||--o{ PEDIDO : realiza
    PEDIDO ||--o{ ITEM_PEDIDO : contem
    PESSOA ||--o{ NEGOCIACAO : inicia
    PESSOA ||--o{ TROCA : participa
