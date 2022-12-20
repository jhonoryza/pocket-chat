# Pocketchat

A basic realtime chat app demo with Pocketbase & Svelte. 

this is a fork from repo: [https://github.com/fireship-io/pocketchat-tutorial](https://github.com/fireship-io/pocketchat-tutorial)

## requirement
- installed pocketbase server
- installed npm and nodejs

## pocketbase setup
- add new collection messages
- add field type and name text min:1 max:255
- add field type relation and name user, choose collection from users 
- adjust api rules messages only admins for update and delete
- adjust api rules messages user = @request.auth.id for create
- adjust api rules messages list/search and view for everyone access
- adjust api rules users view for everyone access

## try in local
- adjust pocketbase.ts file to configure pocketbase server url
- npm install
- npm run dev

## deploy
- npm run build