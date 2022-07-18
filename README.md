# Rolify cancancan Devise

## For creating and assigning roles

> Start rails console by `rails c` then follow the below command

```
# Create user
User.create!(email: "rutik@example.com",password: "password")
User.create!(email: "r@example.com",password: "password")

## For adding role
user.add_role :admin

## For checking whether a user has some role
user.has_role? :admin

## For removing role from a user
user.remove_role :admin

```