import pygame
import random
import sys

pygame.init()

WIDTH = 400
HEIGHT = 300
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Move and Collect")

WHITE = (255, 255, 255)
BLUE = (0, 0, 255)
YELLOW = (255, 255, 0)

player_size = 30
star_size = 20

player_x = WIDTH // 2
player_y = HEIGHT // 2

score = 0

star_x = random.randint(0, WIDTH - star_size)
star_y = random.randint(0, HEIGHT - star_size)

running = True
clock = pygame.time.Clock()

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player_x -= 5
    if keys[pygame.K_RIGHT]:
        player_x += 5
    if keys[pygame.K_UP]:
        player_y -= 5
    if keys[pygame.K_DOWN]:
        player_y += 5

    if player_x < star_x + star_size and player_x + player_size > star_x and player_y < star_y + star_size and player_y + player_size > star_y:
        score += 1
        star_x = random.randint(0, WIDTH - star_size)
        star_y = random.randint(0, HEIGHT - star_size)

    screen.fill(WHITE)
    pygame.draw.rect(screen, BLUE, (player_x, player_y, player_size, player_size))
    pygame.draw.circle(screen, YELLOW, (star_x + star_size // 2, star_y + star_size // 2), star_size // 2)

    font = pygame.font.Font(None, 36)
    text = font.render(f'Score: {score}', True, BLUE)
    screen.blit(text, (10, 10))

    pygame.display.flip()

    clock.tick(30)

pygame.quit()
sys.exit()
