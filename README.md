# minigama
that game about dracon
import pygame
import random

# ініціалізація Pygame
pygame.init()

# Налаштування екрану
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Дракончик Льодовий: Подорож у Мрії")

# Кольори
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
BLUE = (0, 0, 255)
RED = (255, 0, 0)

# Шрифти
font = pygame.font.SysFont('Arial', 30)

# Клас для дракончика
class Dragon:
    def __init__(self, x, y):
        self.image = pygame.Surface((50, 50))
        self.image.fill(BLUE)
        self.rect = self.image.get_rect()
        self.rect.center = (x, y)
        self.speed = 5
        self.gravity = 1
        self.y_velocity = 0
    
    def move(self):
        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            self.rect.x -= self.speed
        if keys[pygame.K_RIGHT]:
            self.rect.x += self.speed
        if keys[pygame.K_UP]:
            self.y_velocity = -10
        self.rect.y += self.y_velocity
        self.y_velocity += self.gravity
        if self.rect.bottom > HEIGHT:
            self.rect.bottom = HEIGHT
            self.y_velocity = 0

    def draw(self, screen):
        screen.blit(self.image, self.rect)

# Основна функція гри
def game_loop():
    dragon = Dragon(WIDTH // 2, HEIGHT - 60)
    clock = pygame.time.Clock()

    running = True
    while running:
        screen.fill(WHITE)
        
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
        
        dragon.move()
        dragon.draw(screen)
        
        # Показати повідомлення
        text = font.render('Подорож дракончика!', True, BLACK)
        screen.blit(text, (10, 10))
        
        pygame.display.flip()
        clock.tick(60)

    pygame.quit()

# Запуск гри
if __name__ == '__main__':
    game_loop()
