```mermaid
---
title: "Models: Related to Partner"
---

erDiagram

    %% N:N 1=<
    Partner ||--o| Users : has
    Partner |o--|| PartnerTags : has
    Partner ||--|o Bank : has
    Partner ||--|o BankAccounts : has
    Bank ||--|o BankAccounts : has


    Users{
        int id PK
        bool active "有効フラグ"
        char company_id FK "*会社ID"
        char login "*ログインID"
        char notification_type "*通知方法"
        char partner_id FK "*連絡先ID"
        char property_account_payable_id FK "*買掛用勘定科目ID"
        char property_account_receivable_idc FK "売掛用勘定科目ID"
    }

    Partner{
        char id PK
        char bank_ids FK "銀行ID"
        char buyer_id FK "購買担当者ID"
        char category_id FK "タグID"
        char name(multi) "名称"
        bool active "有効フラグ"
        char company_id FK "法人ID"
        int is_company "法人フラグ"
        char country_id FK "国ID"
        char state_id FK "都道府県/州ID"
        char city "市区町村"
        char street "住所1"
        char street "住所2"
        char phone "電話番号"
        char email "メールアドレス"
        char mobile "携帯電話"
        char currency_id "通貨ID default=Null"
        bool employee "従業員フラグ"
        char employee_ids "従業員ID"
        %% 意味不明フラグ
        bool is_backlisted
        bool is_public
    }

    Bank{
        %% 支店毎に１レコード 1record per 1 branch
        int id PK
        bool active "有効フラグ"
        char name "名称"
        char bic "銀行識別コード"
        char zip "郵便番号"
        char country_id FK "国ID"
        char state_id FK "都道府県/州ID"
        char city "市区町村"
        char street "住所1"
        char street "住所2"
        char phone "電話番号"
        char email "メールアドレス"
        char display_name "?"
    }

    BankAccounts{
        int id PK
        bool active "有効フラグ"
        char bank_id FK "銀行ID"
        char acc_number "*口座番号"
        char partner_id FK "*口座名義人ID"
        char acc_holder_name "口座名義人読みかな"
        bool allow_out_payment "送金許可フラグ"
        char acc_type "銀行口座タイプ"
        char company_id FK "会社ID？?"
        char currency_id FK "通貨ID set Null"
    }

    PartnerTags{
        int id PK
        bool active "有効フラグ"
        char name "*名称"
        int color "色"
        char parent_id FK "親タグID"
    }




    %% 1:N 0<=
    %% CUSTOMER ||--o{ ORDER : places
    %% CUSTOMER ||--o{ INVOICE : "liable for"
    %% DELIVERY-ADDRESS ||--o{ ORDER : receives

    %% %% 1:N 1=<
    %% INVOICE ||--|{ ORDER : covers
    %% ORDER ||--|{ ORDER-ITEM : includes
    %% PRODUCT-CATEGORY ||--|{ PRODUCT : contains
    %% %% 1:N 
    %% PRODUCT ||--o| ORDER-ITEM : "ordered in"
    %% CUSTOMER {
    %%     type name PK "comment"
    %%     type name FK "コメント"
    %%     type name UK "コメント"
    %%     type name "名称"
    %%     type name
        
    %% }

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
