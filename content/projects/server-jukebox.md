+++
title = "Server Jukebox"
date = 2023-04-02
draft = false
+++

Git Repo: [Link](https://github.com/berinaniesh/server-jukebox)

Server Jukebox, as the name implies is a [jukebox](https://en.wikipedia.org/wiki/Jukebox) for a server (no coins needed though :P). It allows anyone on the local network (or the internet) to queue songs to be played on the server. 

It uses `yt-dlp` to download audio and `mpv` to play the downloaded audio. It also uses a `mariadb` database to keep state. 

## Deploy

+ Clone the [repo](https://github.com/berinaniesh/server-jukebox) and `cd` into it. 
+ Create a copy of `.env.example` to `.env` and make necessary changes. 
+ Install `sqlx-cli` with `cargo install sqlx-cli`
+ Run migrations with `sqlx migrate run`
+ Run the application with `cargo run --release`
+ To deploy as a systemd service, check out [this](https://github.com/berinaniesh/server-jukebox/blob/main/jukebox.service) file in the repo.

## Screenshots

### Web UI
![Screenshot1](/server_jukebox1.png)

### Application Log
![Screenshot2](/server_jukebox2.png)
