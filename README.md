# tile-based-project
my first game project
import pygame
 
# Define some colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
GREEN = (104, 237, 107)
RED = (247, 83, 72)
BLUE = (98, 105, 191)
YELLOW = (222, 235, 42)

deaths = (0)
 
pygame.init()
 
# Set the width and height of the screen [width, height]
size = (700, 500)
screen = pygame.display.set_mode(size)
 
pygame.display.set_caption("My Game")
 
# Loop until the user clicks the close button.
done = False
 
# Used to manage how fast the screen updates
clock = pygame.time.Clock()

all_sprites_list = pygame.sprite.Group()
walls_list = pygame.sprite.Group()
enemy_list = pygame.sprite.Group()
enemy2_list = pygame.sprite.Group()
keys_list = pygame.sprite.Group()


class Character(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image=pygame.Surface((25,25))
        self.image.fill(BLUE)
        self.rect = self.image.get_rect()
        self.rect.y = 0
        self.rect.x = 0
        self.keys = 0

    def update(self):
            key_collision = pygame.sprite.spritecollide(Player1, keys_list, True)
            if key_collision:
                self.keys = self.keys + 1


class EndandStart(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image=pygame.Surface((60,60))
        self.image.fill(GREEN)
        self.rect = self.image.get_rect()
        self.rect.y = 0
        self.rect.x = 0

class Enemy(pygame.sprite.Sprite):
    def __init__(self,x):
        pygame.sprite.Sprite.__init__(self)
        self.image=pygame.Surface((25,25))
        self.image.fill(WHITE)
        self.rect = self.image.get_rect()
        self.rect.y = 20
        self.rect.x = x
        self.damage = 20
        self.x_change = 0
        self.y_change = 5

class Key(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image=pygame.Surface((12,12))
        self.image.fill(YELLOW)
        self.rect = self.image.get_rect()
        self.rect.y = 0
        self.rect.x = 0


font = pygame.font.Font('freesansbold.ttf',20)

txtX = 70
txtY = 40

def showscore(x,y):
    score = font.render("Deaths: " + str(deaths) + "                                                          Keys: " + str(Player1.keys) + "/2"
                , True, (255, 255, 255))
    screen.blit(score, (x, y))




for x in range (110, 610, 75):
    Enemy1 = Enemy(x)
    all_sprites_list.add(Enemy1)
    enemy_list.add(Enemy1)

for x in range (75, 650, 75):
    Enemy1 = Enemy(x)
    Enemy1.rect.y = 455
    all_sprites_list.add(Enemy1)
    enemy_list.add(Enemy1)
    

class Wall(pygame.sprite.Sprite):
    def __init__(self, x, y):
        pygame.sprite.Sprite.__init__(self)
        self.image=pygame.Surface((20,20))
        self.image.fill(RED)
        self.rect = self.image.get_rect()
        self.rect.y =x
        self.rect.x =y


Startblock = EndandStart()
Startblock.rect.y = 420
Startblock.rect.x = 0

Endblock = EndandStart()
Endblock.rect.y = 20
Endblock.rect.x = 640

Player1 = Character()
Player1.rect.y = 440
Player1.rect.x = 17

playerX_change = 0
playerY_change = 0



Key1 = Key()
Key1.rect.x = 343
Key1.rect.y = 450
all_sprites_list.add(Key1)
keys_list.add(Key1)

Key2 = Key()
Key2.rect.x = 343
Key2.rect.y = 43
all_sprites_list.add(Key2)
keys_list.add(Key2)




maps =  [[1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,1,1],
         [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]]


all_sprites_list.add(Startblock)
all_sprites_list.add(Endblock)
all_sprites_list.add(Player1)


for x in range(25):

    for y in range(35):

        if maps [x][y] ==1:
            wall = Wall(x*20, y*20)
            all_sprites_list.add(wall)
            walls_list.add(wall)

    
# -------- Main Program Loop -----------
while not done:
    # --- Main event loop
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            done = True

        if event.type == pygame.KEYDOWN:
               if event.key == pygame.K_a:
                   playerX_change = -2
               if event.key == pygame.K_d:
                   playerX_change = 2
               if event.key == pygame.K_w:
                   playerY_change = -2
               if event.key == pygame.K_s:
                   playerY_change = 2

        if event.type == pygame.KEYUP:
            if event.key == pygame.K_a or event.key == pygame.K_d:
                playerX_change = 0
            if event.key == pygame.K_w or event.key == pygame.K_s:
                playerY_change = 0
     

    Player1.rect.x += playerX_change
    Player1.rect.y += playerY_change

    
    if Player1.rect.x < 0:
        Player1.rect.x = 0
    if Player1.rect.x > 675:
        Player1.rect.x = 675

    wall_stop = pygame.sprite.spritecollide(Player1, walls_list, False)

    if wall_stop:
        Player1.rect.x = Player1.rect.x - playerX_change
        Player1.rect.y = Player1.rect.y - playerY_change

    enemy_collision = pygame.sprite.spritecollide(Player1, enemy_list, False)

    if enemy_collision:
        Player1.rect.y = 435
        Player1.rect.x = 20
        deaths = deaths + 1

    enemy2_collision = pygame.sprite.spritecollide(Player1, enemy2_list, False)

    if enemy2_collision:
          Player1.rect.y = 435
          Player1.rect.x = 20
          deaths = deaths + 1

        

    for enemy in enemy_list:
        enemy.rect.y += enemy.y_change
        if enemy.rect.y >= 460:
            enemy.y_change = -enemy.y_change
        if enemy.rect.y <= 20:
            enemy.y_change = -enemy.y_change


    for enemy2 in enemy2_list:
        enemy2.rect.x += enemy2.x_change
        if enemy2.rect.x >= 615:
            enemy2.x_change = -enemy2.x_change
        if enemy2.rect.x <= 60:
            enemy2.x_change = -enemy2.x_change

    

    screen.fill(BLACK)
 
    # --- Drawing code should go here
 

    all_sprites_list.update()

    all_sprites_list.draw(screen)

    showscore(txtX, txtY)

        # --- Go ahead and update the screen with what we've drawn.
    pygame.display.flip()
 
    # --- Limit to 60 frames per second
    clock.tick(60)

    #endgame
    if Player1.rect.x >= 660 and Player1.keys == 2:

                all_sprites_list = pygame.sprite.Group()
                enemy_list = pygame.sprite.Group()


                for x in range(25):

                    for y in range(35):

                        if maps [x][y] ==1:
                            wall = Wall(x*20, y*20)
                            all_sprites_list.add(wall)
                            walls_list.add(wall)        

                Startblock = EndandStart()
                Startblock.rect.y = 420
                Startblock.rect.x = 0

                Endblock = EndandStart()
                Endblock.rect.y = 20
                Endblock.rect.x = 640

                Player1 = Character()
                Player1.rect.y = 440
                Player1.rect.x = 17

                playerX_change = 0
                playerY_change = 0

                all_sprites_list.add(Startblock)
                all_sprites_list.add(Endblock)
                all_sprites_list.add(Player1)


                class Enemy2(pygame.sprite.Sprite):
                    def __init__(self, y):
                        pygame.sprite.Sprite.__init__(self)
                        self.image=pygame.Surface((25,25))
                        self.image.fill(WHITE)
                        self.rect = self.image.get_rect()
                        self.rect.y = y
                        self.rect.x = 60
                        self.damage = 20
                        self.x_change = 1
                        
                for y in range (90, 430, 75):
                       enemy2 = Enemy2(y)
                       all_sprites_list.add(enemy2)
                       enemy2_list.add(enemy2)
                for y in range (128, 400, 75):
                       enemy2 = Enemy2(y)
                       enemy2.rect.x = 614
                       all_sprites_list.add(enemy2)
                       enemy2_list.add(enemy2)
                for x in range (110, 610, 75):
                    Enemy1 = Enemy(x)
                    all_sprites_list.add(Enemy1)
                    enemy_list.add(Enemy1)

                for x in range (75, 650, 75):
                    Enemy1 = Enemy(x)
                    Enemy1.rect.y = 455
                    all_sprites_list.add(Enemy1)
                    enemy_list.add(Enemy1)

                Key1 = Key()
                Key1.rect.x = 500
                Key1.rect.y = 450
                all_sprites_list.add(Key1)
                keys_list.add(Key1)

                Key2 = Key()
                Key2.rect.x = 207
                Key2.rect.y = 43
                all_sprites_list.add(Key2)
                keys_list.add(Key2)

                if Player1.rect.x >= 660 and Player1.keys == 2:
                    done = True

       
        
# Close the window and quit.
pygame.quit()
