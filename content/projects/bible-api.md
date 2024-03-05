+++
title = "Bible API"
date = 2023-10-02
draft = false
+++

Git Repo: [Link](https://github.com/berinaniesh/bible-api)

Deployed at: [Link](https://api.bible.berinaniesh.xyz/docs)

Bible API as the name implies, is an API server which serves bible verses over REST endpoints. To avoid licensing issues, only bibles in the Public Domain are available.

It uses a postgresql database and is written using [Actix Web](https://github.com/actix/actix-web) and [SQLx](https://github.com/launchbadge/sqlx). 

Right now, two frontends get data from the API. 

+ [UI 1](https://bible.berinaniesh.xyz) - SSR with hydration, fast and responsive UI (prerendering, fetch on hover, etc).
+ [UI 2](https://scripture.berinaniesh.xyz) - SSG, more mature UI. 

## License

The server, the data and the bibles are all in the public domain and so feel free to self host, distribute everything. 
