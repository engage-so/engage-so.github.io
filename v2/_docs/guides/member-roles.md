---
layout: docs
page: member-roles
title: Team member roles
description: Engage supports different team member roles to manage access and privileges.
---
# Team member roles

Engage supports adding team members to an account. Each member can be assigned any of the four available roles:

- `Admin`
- `Manager`
- `Developer`
- `Member`

These roles define what what they can do. There is a fifth `Owner` role that is automatically assigned to the account creator. This role grants all privilege to the account, including deletion. The role can be transfered by its owner to another member. However, only one member of a team can have the role at a given time. On transfer, the role of the member transferring will be changed to `admin`.

## Admin
- Cannot delete the account. (Only the account creator can delete an account).
- Can do everything else
	
## Manager
- Cannot grant admin access to another team mate.
- Cannot delete the account
- Can do everything else

## Developer
- Has full access to templates
- Has full access to transactional email analytics
- Has full access to users
- Has full access to lists
- Can view broadcasts
- Can view segments
- Cannot invite, edit role or remove team members
- Cannot create, update or send broadcast
- Cannot create, update or delete segments

## Member
- Cannot perform any create, update or delete actions. Can only view all modules on the dashboard. 
- Cannot view transactional email body
