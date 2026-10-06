# README

## Members Only

An exclusive clubhouse where members write anonymous posts. Anyone can read the posts, but only signed-in members can see who wrote them.


Features
User sign up, sign in, and sign out with Devise
Signed-in members can create new posts (title and body)
Public post board, newest posts first
Conditional authorship display: the author's name appears only when a user is signed in
new and create actions protected by authentication; the author is set server-side from current_user, so a post can't be attributed to someone else
Eager loading (includes) to avoid N+1 queries on the index page
Model validation (title presence) backed by a database NOT NULL constraint

## Tech stack
Ruby on Rails
PostgreSQL
Devise (authentication)
ERB views

## Data model
users                          posts
-----                          -----
id                             id
name                           title
email                          body
encrypted_password             user_id  -> users.id (foreign key)
...                            timestamps

User has_many :posts
Post belongs_to :user

## Getting started

Prerequisites: Ruby, Rails, and PostgreSQL installed and running.

bash
git clone https://github.com/<your-username>/members-only.git
cd members-only
bundle install
bin/rails db:setup
bin/rails server

Then open http://localhost:3000, sign up, and post your first secret.

## How it works
PostsController uses before_action :authenticate_user!, only: [:new, :create] so only signed-in users can post.
create builds the post through the association (current_user.posts.build), which fills in user_id automatically. Strong parameters allow only title and body.
The index view checks user_signed_in? before rendering post.user.name.

## What I learned
The difference between authentication (who are you?) and authorization (what are you allowed to see or do?)
Using Devise and customising it (permitting an extra name parameter on sign up)
Why foreign keys live on the "many" side of a one-to-many relationship
Building records through associations and using strong parameters to prevent tampering
Spotting and fixing N+1 queries with includes

## Possible future improvements

Styling and a responsive layout

##License

This project is for learning purposes.
