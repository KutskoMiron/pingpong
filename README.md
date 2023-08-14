from pygame import*

font.init()
font = font.SysFont('Arial',35)
lose1 = font.render('PLAYER 1 LOSE!', True, (180, 0, 0))
lose2 = font.render('PLAYER 2 LOSE!', True, (180, 0, 0))


class GameSprite(sprite.Sprite):
    def __init__(self, player_image, player_x, player_y, player_speed, wight, height):
        super().__init__()
        self.image = transform.scale(image.load(player_image), (wight, height))
        self.speed = player_speed
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y = player_y

    def reset(self):
        window.blit(self.image, (self.rect.x, self.rect.y))


class Player(GameSprite):
    def update_l(self):
        keys = key.get_pressed()
        if keys[K_UP] and self.rect.y > 5:
            self.rect.y -= self.speed
        if keys[K_DOWN] and self.rect.y <350:
            self.rect.y += self.speed

    def update_2(self):
        keys = key.get_pressed()
        if keys[K_w] and self.rect.y > 5:
            self.rect.y -= self.speed
        if keys[K_s] and self.rect.y <350:
            self.rect.y += self.speed

speed_x = 5
speed_y = 5

back = (200, 255, 255)

background = transform.scale(image.load('151843-gory-ozero-otrazhenie-gornyj_relef-prirodnyj_landshaft-550x310.jpg'), (700, 500))
window = display.set_mode((700, 500))
window.fill(back)
display.set_caption('Тенис')
game = True
finish = False

ball = GameSprite('tenis_ball.png', 200, 200, 4, 50, 50)
racket1 = Player('racket (1).png', 600, 200, 4, 50, 150)
racket2 = Player('racket (1).png', 30, 200, 4, 50, 150)

while game:
    for e in event.get():
        if e.type == QUIT:
            game = False
    if  not finish:
        window.fill(back)
        ball.reset()
        racket1.update_l()
        racket1.reset()
        racket2.update_2()
        racket2.reset()
        ball.rect.x += speed_x
        ball.rect.y += speed_y
        if ball.rect.y> 450 or ball.rect.y <0:
            speed_y *= -1  
        if sprite.collide_rect(racket1, ball) or sprite.collide_rect(racket2, ball):
            speed_x *= -1   
        if ball.rect.x > 700:
            finish = True
            window.blit(lose2, (200, 200))
        if ball.rect.x <0:
            finish = True
            window.blit(lose1, (200, 200))

    display.update()
    time.delay(10)
