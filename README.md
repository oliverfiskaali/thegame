# thegame
Pygame-projekt

import pygame
pygame.init()

class board():
    def __init__(self, boxL, boxH):
        self.boxL = boxL
        self.boxH = boxH
    def draw(self,screen):
        self.screen = screen
        image = pygame.image.load("SOMETHING")
        image.blit(screen,(self.boxL,self.boxH))

class spiller():
    def __init__(self, color, x, y, width, height, vel, jumplength, jumpdowntime):
        self.color = color
        self.x = x
        self.y = y
        self.width = width
        self.height = height
        self.vel = vel
        self.jump = False
        self.run = True
        self.jumplength = jumplength
        self.jumpdowntime = jumpdowntime

pygame.display.set_caption("Road to heaven")

Pink = (240, 70, 220)
Player = spiller((255,0,0), 0, 0, 35, 80, 1, 150, 1000)
screen = board(1000, 600)
win = pygame.display.set_mode((screen.boxL, screen.boxH))

while Player.run:
    pygame.time.delay(0)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame = False

    keys = pygame.key.get_pressed()

    if keys[pygame.K_a] and Player.x > 0:
        Player.x -= Player.vel

    if keys[pygame.K_d]and Player.x < screen.boxL - (Player.width):
        Player.x += Player.vel

    if keys[pygame.K_w]and Player.y > 0:
        Player.y -= Player.vel

    if keys[pygame.K_s] and Player.y < screen.boxH - (Player.height):
        Player.y += Player.vel

    if keys[pygame.K_SPACE] and keys[pygame.K_w]:
        if Player.jump == False and keys[pygame.K_SPACE] and keys[pygame.K_w]:
            starttime = pygame.time.get_ticks()
            Player.y -= Player.jumplength
            Player.jump = True
            if Player.y < 0:
                Player.y = 0


    if keys[pygame.K_SPACE] and keys[pygame.K_d]:
        if Player.jump == False and keys[pygame.K_SPACE] and keys[pygame.K_d]:
            starttime = pygame.time.get_ticks()
            Player.x += Player.jumplength
            Player.jump = True
            if Player.x > screen.boxL-Player.width:
                Player.x = screen.boxL-Player.width

    if keys[pygame.K_SPACE]and keys[pygame.K_a]and Player.x > 0:
        if Player.jump == False and keys[pygame.K_SPACE] and keys[pygame.K_a]:
            starttime = pygame.time.get_ticks()
            Player.x -= Player.jumplength
            Player.jump = True
            if Player.x < 0:
                Player.x = 0

    if keys[pygame.K_SPACE]and keys[pygame.K_s]:
        if Player.jump == False and keys[pygame.K_SPACE] and keys[pygame.K_s]:
            starttime = pygame.time.get_ticks()
            Player.y += Player.jumplength
            Player.jump = True
            if Player.y > screen.boxH-Player.height:
                Player.y = screen.boxH-Player.height

    if Player.jump == True and pygame.time.get_ticks() - starttime >= Player.jumpdowntime:
        Player.jump = False

    win.fill((0, 0, 0,))
    pygame.draw.rect(win, Player.color, (Player.x, Player.y, Player.width, Player.height))
    pygame.display.update()



pygame.quit()
