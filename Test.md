```mermaid
---
title: "タイトル"
---

erDiagram

    %% N:N 1=<
    CUSTOMER }|..|{ DELIVERY-ADDRESS : has
    %% 1:N 0<=
    CUSTOMER ||--o{ ORDER : places
    CUSTOMER ||--o{ INVOICE : "liable for"
    DELIVERY-ADDRESS ||--o{ ORDER : receives

    %% 1:N 1=<
    INVOICE ||--|{ ORDER : covers
    ORDER ||--|{ ORDER-ITEM : includes
    PRODUCT-CATEGORY ||--|{ PRODUCT : contains
    %% 1:N 
    PRODUCT ||--o| ORDER-ITEM : "ordered in"
    CUSTOMER {
        type name PK "comment"
        type name FK "コメント"
        type name UK "コメント"
        type name "名称"
        type name
        
    }

%% 左	右	意味
%% ｜o	o｜	ゼロか一対一
%% ｜｜	｜｜	一か一対一
%% }o	o{	ゼロか一対多
%% }｜	｜{	一対多か多対多
%% --:

%% 略語	名称	名称（日本語）
%% PK	primary key	主キー
%% FK	foreign key	外部キー
%% UK	unique key	一意キー
