# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...


# テーブル設計

# usersテーブル

| Column             | type    | option                   |
| ------------------ | ------- | ------------------------ |
| email              | string  | null: false unique: true |
| encrypted_password | string  | null: false              |
| name               | string  | null: false              |
| profile            | text    |                          |

- has_many :final_goals
- has_many :sub_goals
- has_many :final_goal_comments
- has_many :sub_goal_comments
- has_many :favorites




# final_goalsテーブル

| Column             | type          | option                         |
| ------------------ | ------------- | ------------------------------ |
| title              | string        | null: false                    |
| target_date        | date          | null: false                    |
| user               | references    | null: false, foreign_key: true |

- belongs_to :user
- has_many :final_goal_comments
- has_many :sub_goals
- has_many :favorites

# sub_goalsテーブル
| Column             | type          | option                         |
| ------------------ | ------------- | ------------------------------ |
| title              | string        | null: false                    |
| text               | text          | null: false                    |
| target_date        | date          | null: false                    |
| user               | references    | null: false, foreign_key: true |
| final_goal         | references    | null: false, foreign_key: true |

- belongs_to :user
- belongs_to :final_goal
- has_many :sub_goal_comments

# final_goal_commentsテーブル
| Column             | type          | option                         |
| ------------------ | ------------- | ------------------------------ |
| comment            | text          | null: false                    |
| user               | references    | null: false, foreign_key: true |
| final_goal         | references    | null: false, foreign_key: true |

- belongs_to :user
- belongs_to :final_goal

# sub_goal_commentsテーブル
| Column             | type          | option                         |
| ------------------ | ------------- | ------------------------------ |
| comment            | text          | null: false                    |
| user               | references    | null: false, foreign_key: true |
| sub_goal           | references    | null: false, foreign_key: true |

- belongs_to :user
- belongs_to :sub_goal

# favoritesテーブル
| Column             | type          | option                         |
| ------------------ | ------------- | ------------------------------ |
| user               | references    | null: false, foreign_key: true |
| final_goal         | references    | null: false, foreign_key: true |

- belongs_to :user
- belongs_to :final_goal