# Snake Game
## main
### Screen
```python
<?python
    screen = Screen()
    screen.setup(width=600, height=600)
    screen.bgcolor("black")
    screen.title("Snake Game")
    screen.tracer(0);
?>
```
Screen define todas las características que va a tener la pantalla de la aplicación importado también con ayuda de librerías

### Detección de la comida
```python
    if snake.head.distance(food) < 15:
        food.refresh()
        snake.extend()
        scoreboard.increase_score()
 ```
Todo lo contenido en este if determina el choque de la serpiente con la comida

### Detección de las paredes 
```python
    if snake.head.xcor() > 280 or snake.head.xcor() < -280 or snake.head.ycor() > 280 or snake.head.ycor() < -280:
        game_is_on = False
        scoreboard.game_over()
 ```
Este if determina el golpe de la serpiente contra las paredes de la pantalla

### Detección de las paredes (terminar juego)
```python
    for segment in snake.segments:
        if segment == snake.head:
            pass
        elif snake.head.distance(segment) < 10:
            game_is_on = False
            scoreboard.game_over()
            screen.exitonclick()
 ```
Este if determina que si la cabeza de la serpiente cumple con el anterior if debe terminar el juego 


## food
### creacion de la comida 
```python
<?python
    class Food(Turtle):
    def __init__(self):
        super().__init__()
        self.shape("circle")
        self.penup()
        self.shapesize(stretch_len=0.5, stretch_wid=0.5)
        self.color("blue")
        self.speed("fastest")
        self.refresh()
?>
```
En esta clase creamos y configuramos las carateristicas que tendra la comida 

### Reacomodar la comida 
```python
<?python
    def refresh(self):
        random_x = random.randint(-280, 280)
        random_y = random.randint(-280, 280)
        self.goto(random_x, random_y)
?>
```
Aca definimos el limite en el que saldra la comida asi como ramdomizar el spawneo de la misma


## scoreboard
### Serpiente 
```python
<?python
    class Scoreboard(Turtle):
    def __init__(self):
        super().__init__()
        self.score = 0
        self.color("white")
        self.penup()
        self.goto(0, 270)
        self.hideturtle()
        self.update_scoreboard()
?>
```
Creamos y definimos las caracteristicas de la serpiente

###  Actualizacion de score 
```python
<?python
    def update_scoreboard(self):
        self.write(f"Score: {self.score}",align=ALIGNMENT, font=FONT)
```
Definimos el lugar donde estara ubicado la tabla de puntaje

###  Game over 
```python
<?python
    def game_over(self):
        self.goto(0, 0)
        self.write("GAME OVER",
                   align=ALIGNMENT, font=FONT)

```
definimos en que momento, en donde y por que aparecera el catel de game over

###  Puntos por comida 
```python
<?python
    def increase_score(self):
        self.score += 1
        self.clear()
        self.update_scoreboard()
```
Definimos la funcion para que cada que 1 fruta sea comida debe agregar 1 punto al puntaje


## Snake
### Pocision inicial
```python
<?python
    STARTING_POSITIONS = [(0, 0), (-20, 0), (-40,0)]
?>
```
Definimos el lugar donde la serpiente empezara el juego 

### segmentos de las serpiente 
```python
<?python
    class Snake:
        def __init__(self):
            self.segments = []
            self.create_snake()
            self.head = self.segments[0]
?>
```
Creacion de los segmentos y definicion de la cabeza 

### Creacion de la serpiente
```python
<?python
    def create_snake(self):
        for position in STARTING_POSITIONS:
            self.add_segment(position)
?>
```
Se acomodan los segmentos donde definimos como posicion inicial

### Agregar un segmento a la serpiente 
```python
<?python
    def add_segment(self, position):
        new_segment = Turtle("square")
        new_segment.color("white")
        new_segment.penup()
        new_segment.goto(position)
        self.segments.append(new_segment)
    def extend(self):
        self.add_segment(self.segments[-1].position())
?>
```
Definimos que cada punto es una extencion a la serpiente y en que lugar de los segmentos debe situarse 

### Movimiento constante
```python
<?python
    def move(self):
        for seg_num in range(len(self.segments)- 1, 0, -1):
            new_x = self.segments[seg_num -1].xcor()
            new_y = self.segments[seg_num -1].ycor()
            self.segments[seg_num].goto(new_x,new_y)
        self.head.forward(MOVE_DISTANCE)
?>
```
definimos que cuando empieze el juego y hasta que termine la serpiuente debe estar siempre en movimineto

### Controles 
```python
<?python
    def up(self):
        if self.head.heading() != DOWN:
            self.head.setheading(UP)

    def down(self):
        if self.head.heading() != UP:
            self.head.setheading(DOWN)

    def left(self):
        if self.head.heading() != RIGHT:
            self.head.setheading(LEFT)

    def right(self):
        if self.head.heading() != LEFT:
            self.head.setheading(RIGHT)
?>
```
Definimos los controles para el juego 
