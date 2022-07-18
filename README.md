# Rolify cancancan Devise

## For creating and assigning roles

> Start rails console by `rails c` then follow the below command

```
# Create user
User.create!(email: "rutik@example.com",password: "password")
User.create!(email: "r@example.com",password: "password")

# Find The user
u = User.find(1)
u2 = User.find(2)

## For adding role
u.add_role :admin

## For checking whether a user has some role
u.has_role? :admin

## For removing role from a user
u.remove_role :admin

```

## Add the resourcify method in all models in which you want to put a role on.
```
class Model < ActiveRecord::Base
  resourcify
end
```

## Edit Ability, add below code in initializer method
```
if user.has_role? :admin
  can :manage, :all
else
  can :read, :all
  can :edit, User if user.has_role?(:editor, User)
end
```

## Check if the user has admin rights
```
a = Ability.new(u)
a.can? :manage, :all
# it returns - true

a2 = Ability.new(u2)
a2.can? :manage, :all
# it returns - false, as nobody expect admin can manage

a2.can? :read, :all
# it returns - true, as other user can read

a2.can? :edit, User
# it returns - true

a2.can? :edit, :all
# it returns - false, as it only edit user
```