# -*- coding: utf-8 -*-
"""
Created on Thu Nov 24 22:24:05 2022

"""


import os  
import turtle  
import playsound




sonido= 'sonido.mp3'
    
screen_1 = turtle.Screen()  
screen_1.title("Juego de Ping Pong")  
screen_1.bgcolor("black")  
screen_1.setup(width = 1050, height = 650)  
   
   
# Jugador_1
jugador_1_paddle = turtle.Turtle()  
jugador_1_paddle.speed(12)  
jugador_1_paddle.shape("square")  
jugador_1_paddle.color("Red")  
jugador_1_paddle.shapesize(stretch_wid = 6, stretch_len = 2)  
jugador_1_paddle.penup()  
jugador_1_paddle.goto(-400, 0)  
   
   
# Jugador_2
jugador_2_paddle = turtle.Turtle()  
jugador_2_paddle.speed(12)  
jugador_2_paddle.shape("square")  
jugador_2_paddle.color("Blue")  
jugador_2_paddle.shapesize(stretch_wid = 6, stretch_len = 2)  
jugador_2_paddle.penup()  
jugador_2_paddle.goto(400, 0)  
   
   
bola = turtle.Turtle()  
bola.speed(45)  
bola.shape("circle")  
bola.color("white")  
bola.penup()  
bola.goto(0, 0)  
bola.dx = 5  
bola.dy = -5  
   
   
# Puntaje
jugador_1 = 0  
jugador_2 = 0  
   
   
sketch_1 = turtle.Turtle()  
sketch_1.speed(0)  
sketch_1.color("white")  
sketch_1.penup()  
sketch_1.hideturtle()  
sketch_1.goto(0, 260)  
sketch_1.write("Jugador 1 : 0    Jugador 2: 0",  
             align = "center", font = ("Courier", 24, "normal"))  
   
   
  
def paddle_L_up():  
    y = jugador_1_paddle.ycor()  
    y += 20  
    jugador_1_paddle.sety(y)  
   
   
def paddle_L_down():  
    y = jugador_1_paddle.ycor()  
    y -= 20  
    jugador_1_paddle.sety(y)  
   
   
def paddle_R_up():  
    y = jugador_2_paddle.ycor()  
    y += 20  
    jugador_2_paddle.sety(y)  
   
   
def paddle_R_down():  
    y = jugador_2_paddle.ycor()  
    y -= 20  
    jugador_2_paddle.sety(y)  
   
   
# Controles 
screen_1.listen()  
screen_1.onkeypress(paddle_L_up, "w")  
screen_1.onkeypress(paddle_L_down, "s")  
screen_1.onkeypress(paddle_R_up, "Up")  
screen_1.onkeypress(paddle_R_down, "Down")  
   
   
while True:  
    screen_1.update()  
   
    bola.setx(bola.xcor() + bola.dx)  
    bola.sety(bola.ycor() + bola.dy)  
   
      
    if bola.ycor() > 280:  
        bola.sety(280)  
        bola.dy *= -1  
   
    if bola.ycor() < -280:  
        bola.sety(-280)  
        bola.dy *= -1  
   
    if bola.xcor() > 500:  
        bola.goto(0, 0)  
        bola.dy *= -1  
        jugador_1 += 1  
        sketch_1.clear()  
        sketch_1.write("Jugador 1 : {}    Jugador 2: {}".format(  
                      jugador_1, jugador_2), align = "center",  
                      font = ("Courier", 24, "normal"))  
   
    if bola.xcor() < -500:  
        bola.goto(0, 0)  
        bola.dy *= -1  
        jugador_2 += 1  
        sketch_1.clear()  
        sketch_1.write("Jugador 1 : {}    Jugador 2: {}".format(  
                                 jugador_1, jugador_2), align = "center",  
                                 font = ("Courier", 24, "normal"))  
   
     
    if (bola.xcor() > 360 and  
                        bola.xcor() < 370) and (bola.ycor() < jugador_2_paddle.ycor() + 40 and  
                        bola.ycor() > jugador_2_paddle.ycor() - 40):  
                        playsound(sonido) 
                        bola.setx(360)  
                        bola.dx *= -1  
          
    if (bola.xcor() < -360 and  
                       bola.xcor() > -370) and (bola.ycor() < jugador_1_paddle.ycor() + 40 and  
                       bola.ycor() > jugador_1_paddle.ycor() - 40):
                       playsound(sonido)
                       bola.setx(-360)  
                       bola.dx *= -1