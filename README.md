# warsawjs-workshop-5-chat

## Warsztat
Repozytorium szkoleniowe. Zawiera zbiór branchy, na których został przedstawiony proces budowania aplikacji czatu w opraciu o web sockety w środowisku node.
Aby rozpocząć wybierz kolejność implementacji:
- serwer
- client

Po wybraniu przejdź odpowiednio do brancha server-milestone#0-initial dla serwera
albo client-milestone#0-initial
i zacznij realizować cele przedstawione w README. Każdy branch posiada także rozwiązanie referencyjne.

## Testowanie serwera czatu

Aby uruchomić serwer czatu należy po sklonowaniu repozytorium zainstalować niezbędne zależności dla serwera:

    $ npm i

Następnie uruchomić serwer poprzez wywołanie skrypty npm:

    $ npm start

Na koniec przejść do przeglądarki i odpalić adres localhost:30001

## Testowanie klienta

Aby uruchomić klienta terminalowego należy po sklonowaniu repozytorium przejść do folderu client

    $ cd client

Następnie zainstalować wymagane zależności:

    $ npm i

Odpalić klienta z połączeniem do serwera lokalnego:

    $ npm start

Albo odpalić do serwera zdalnego:

    $ npm run connect:heroku
    

# workshop FAQ

## biblioteki

server

- [express](https://github.com/expressjs/express)

- [socket.io](https://github.com/socketio/socket.io)

- [bcrypt](https://github.com/kelektiv/node.bcrypt.js)

- [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken)


client

- [socket.io-client](https://github.com/socketio/socket.io-client)

- [blessed](https://github.com/chjj/blessed)

- [react-blessed](https://github.com/Yomguithereal/react-blessed)


dev

- [nodemon](https://github.com/remy/nodemon)

# cheatset

## http

Utworzenie serwera http

````
http.createServer([requestListener])
````

## express

Nasłuchiwanie na żądanie typu `GET`

````
app.get(path, callback [, callback ...])
````

## bcrypt

Tworzenie hasha

````
bcrypt.hash("bacon", SALT, null, (err, hash) => {});
````

Weryfikacja hasha

````
bcrypt.compare("bacon", hash, (err, res) => {});
````

## jsonwebtoken

Tworzenie nowego tokena w oparciu o obiekt `CLAIMS` i `SECRET`

````
jwt.sign(CLAIMS, SECRET, (token) => { ... })
````

Weryfikacja tokena w oparciu o `SECRET`

````
const verified = jwt.verify(token, SECRET);
````

## socket.io

Dołączenie do pokoju

    socket.join(ROOM);


Opuszczenie pokoju

    socket.leave(ROOM);


Emitowanie do wysyłającego

    socket.emit(EVENT, MESSAGE);


Emitowanie do wszystkich w pokoju

    socket.broadcast.on(ROOM).emit(EVENT, MESSAGE);


Emitowanie do wszystkich w pokoju z wyjątkiem wysyłającego

    socket.broadcast.to(ROOM).emit(EVENT, MESSAGE);


do wszystkich poza wysyłającym

    socket.broadcast.emit(EVENT, MESSAGE);


do wszystkich użytkowników poza wysyłającym znajdujących się w konkretnym pokoju

    socket.to(ROOM).emit(EVENT, MESSAGE);


do więcej niż jednego pokoju

    socket.to(ROOM1).to(ROOM2).emit(EVENT, MESSAGE);


do konkretnego użytkownika w oparciu o id jego socketa

    socket.to(SOCKET.ID).emit(EVENT, MESSAGE);


do wszystkich w pokoju

    io.in(ROOM).emit(EVENT, MESSAGE);

do wszystkich

    io.local.emit(EVENT, MESSAGE);

## socket.io-client

Utworzenie socketa połączonego do wskazanego hosta

````
const socket = io('http://localhost');
````

Obsługa zdarzeń analogiczna do serwera

## react-blessed

Przykład użycia:

````
import React, {Component} from 'react';
import blessed from 'blessed';
import {render} from 'react-blessed';

// Rendering a simple centered box
class App extends Component {
  render() {
    return (
      <box top="center"
           left="center"
           width="50%"
           height="50%"
           border={{type: 'line'}}
           style={{border: {fg: 'blue'}}}>
        Hello World!
      </box>
    );
  }
}

// Creating our screen
const screen = blessed.screen({
  autoPadding: true,
  smartCSR: true,
  title: 'react-blessed hello world'
});

// Adding a way to quit the program
screen.key(['escape', 'q', 'C-c'], function(ch, key) {
  return process.exit(0);
});

// Rendering the React app using our screen
const component = render(<App />, screen);
````