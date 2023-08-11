from pygame import*


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
        if keys[K_w] and self.rect.y > 5:
            self.rect.y -= self.speed
        if keys[K_s] and self.rect.y <350:
            self.rect.y += self.speed

    def update_2(self):
        keys = key.get_pressed()
        if keys[K_UP] and self.rect.y > 5:
            self.rect.y -= self.speed
        if keys[K_DOWN] and self.rect.y <350:
            self.rect.y += self.speed



back = (200, 255, 255)

background = transform.scale(image.load('151843-gory-ozero-otrazhenie-gornyj_relef-prirodnyj_landshaft-550x310.jpg'), (700, 500))
window = display.set_mode((700, 500))
window.fill(back)
display.set_caption('Тенис')
game = True

ball = GameSprite('tenis_ball.png', 200, 200, 4, 50, 50)
racket1 = Player('racket (1).png', 600, 200, 4, 50, 150)
racket2 = Player('racket (1).png', 30, 200, 4, 50, 150)

while game:
    for e in event.get():
        if e.type == QUIT:
            game = False
    window.fill(back)
    ball.reset()
    racket1.update_l()
    racket1.reset()
    racket2.update_2()
    racket2.reset()
    display.update()
    time.delay(10)


display.update()
