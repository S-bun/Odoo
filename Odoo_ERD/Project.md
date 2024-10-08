```mermaid
---
title: "Models: Related to Project"
---



erDiagram

    project_project ||--o| account_analytic_account : has
    account_analytic_account ||--|| budget_analytic : has
    budget_analytic ||--o| budget_line : has

    project_project{
        int id PK "データベースID"
        ind account_id FK "account_analytic_account_id"
        int alias_id FK
        int documents_folder_id FK
        char sale_line_id FK
        char reinvoiced_sale_order_id FK
        char x_plan2_id FK
        char x_plan3_id FK
        int sequence
        char partner_id
        char company_id
        int color
        char user_id
        int stage_id
        date last_update_id
        date create_uid
        int write_uid
        char access_token
        char privacy_visibility "master"
        char rating_status
        char rating_status_period "master"
        char last_update_status
        date date_start
        date date
        json name "en_US: 内部"
        json label_tasks "en_US: Tasks"
        char task_properties_definition
        char description
        bool active
        bool allow_task_dependencies
        bool allow_milestones
        bool rating_active
        datetime rating_request_deadline
        datetime create_date
        datetime write_date
        bool use_documents
        bool allow_timesheets
        char allocated_hours
        char allow_billable
        char timesheet_product_id
        char billing_type "master"
    }

    account_analytic_account{
        int id PK "Data base ID"
        int plan_id FK "budget_analytic_id(databaseid)"
        int root_plan_id FK
        char company_id FK
        char partner_id FK
        char create_uid FK
        char write_uid FK
        int code
        json name "en_US:name txt"
        bool active
        datetime create_date
        datetime write_date
    }

    budget_analytic{
        int id PK
        char parent_id FK
        int user_id FK
        int company_id FK
        int create_uid Fk
        int write_uid FK
        char name
        char state "master"
        char budget_type "master"
        date date_from
        date date_to
        datetime create_date
        datetime write_date
    }

    budget_line{
        int id PK
        int account_id FK "account_analytic_account.id"
        int budget_analytic_id FK "budget_analytic.id"
        int sequence
        int company_id FK
        int create_uid Fk
        int write_uid FK
        char budget_analytic_state "master"
        date date_from
        date date_to
        datetime create_date
        datetime write_date
        char x_plan2_id FK
        char x_plan3_id FK
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
