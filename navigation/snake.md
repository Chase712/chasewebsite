---
layout: base
title: Snake
permalink: /snake/
---

<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background-color: #282c34;
        color: white;
        text-align: center;
    }
    .wrap {
        margin: 0 auto;
    }
    canvas {
        display: none;
        border: 10px solid #FFFFFF;
    }
    canvas:focus {
        outline: none;
    }
    /* Screen styles */
    #gameover p, #setting p, #menu p {
        font-size: 20px;
    }
    #gameover a, #setting a, #menu a {
        font-size: 30px;
        display: block;
        text-decoration: none;
        color: white;
    }
    #gameover a:hover, #setting a:hover, #menu a:hover {
        cursor: pointer;
    }
    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before {
        content: ">";
        margin-right: 10px;
    }
    #menu {
        display: block;
    }
    #gameover, #setting {
        display: none;
    }
    #setting input {
        display: none;
    }
    #setting label {
        cursor: pointer;
        padding: 5px 10px;
        border: 1px solid white;
        margin: 5px;
    }
    #setting input:checked + label {
        background-color: #FFF;
        color: #000;
    }
</style>

<h2>Snake</h2>
<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Score: <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align: center;">
        <!-- Main Menu -->
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press <span style="background-color: #FFFFFF; color: #000000">space</span> to begin</p>
            <a id="new_game" href="#" class="link-alert">New Game</a>
            <a id="
