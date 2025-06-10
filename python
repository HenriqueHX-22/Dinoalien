import pygame
import random
import sys

# Inicializar o pygame
pygame.init()

# Configurações da tela
LARGURA = 800
ALTURA = 600
tela = pygame.display.set_mode((LARGURA, ALTURA))
pygame.display.set_caption("Aliens em Dinossauros no Espaço")

# Cores
PRETO = (0, 0, 0)
BRANCO = (255, 255, 255)
AMARELO = (255, 255, 0)
VERDE = (0, 255, 0)
ROXO = (128, 0, 128)

# Classe do Jogador (Alien em Dinossauro)
class Jogador(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(VERDE)
        self.rect = self.image.get_rect()
        self.rect.centerx = LARGURA // 2
        self.rect.bottom = ALTURA - 10
        self.velocidade_x = 0
        self.pontuacao = 0
        
        # Desenhar um dinossauro simples
        pygame.draw.rect(self.image, ROXO, (10, 20, 30, 20))  # Corpo
        pygame.draw.rect(self.image, ROXO, (5, 15, 10, 10))   # Cabeça
        pygame.draw.rect(self.image, VERDE, (15, 10, 5, 5))    # Olho alien
        
    def update(self):
        self.velocidade_x = 0
        teclas = pygame.key.get_pressed()
        if teclas[pygame.K_LEFT]:
            self.velocidade_x = -5
        if teclas[pygame.K_RIGHT]:
            self.velocidade_x = 5
        self.rect.x += self.velocidade_x
        
        # Manter o jogador na tela
        if self.rect.left < 0:
            self.rect.left = 0
        if self.rect.right > LARGURA:
            self.rect.right = LARGURA

# Classe da Banana
class Banana(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((20, 20))
        self.image.fill(AMARELO)
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, LARGURA - self.rect.width)
        self.rect.y = random.randint(-100, -40)
        self.velocidade_y = random.randint(1, 4)
        
        # Desenhar uma banana simples
        pygame.draw.arc(self.image, (139, 69, 19), [0, 0, 20, 20], 0.5, 2.5, 3)

# Classe da Estrela (para fundo)
class Estrela(pygame.sprite.Sprite):
    def __init__(self):
        super().__init__()
        self.image = pygame.Surface((2, 2))
        self.image.fill(BRANCO)
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, LARGURA)
        self.rect.y = random.randint(0, ALTURA)
        self.velocidade_y = random.randint(1, 3)
        
    def update(self):
        self.rect.y += self.velocidade_y
        if self.rect.top > ALTURA:
            self.rect.y = random.randint(-50, -10)
            self.rect.x = random.randint(0, LARGURA)

# Grupos de sprites
todos_sprites = pygame.sprite.Group()
bananas = pygame.sprite.Group()
estrelas = pygame.sprite.Group()

# Criar jogador
jogador = Jogador()
todos_sprites.add(jogador)

# Criar estrelas de fundo
for i in range(100):
    estrela = Estrela()
    todos_sprites.add(estrela)
    estrelas.add(estrela)

# Relógio para controlar FPS
relogio = pygame.time.Clock()
fonte = pygame.font.SysFont(None, 36)

# Temporizador para bananas
tempo_banana = 0

# Loop principal do jogo
rodando = True
while rodando:
    # Manter o loop rodando na velocidade correta
    relogio.tick(60)
    
    # Processar eventos
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            rodando = False
    
    # Atualizar
    todos_sprites.update()
    
    # Adicionar novas bananas
    tempo_banana += 1
    if tempo_banana > 60:  # A cada segundo aproximadamente
        nova_banana = Banana()
        todos_sprites.add(nova_banana)
        bananas.add(nova_banana)
        tempo_banana = 0
    
    # Verificar colisões entre jogador e bananas
    colisoes = pygame.sprite.spritecollide(jogador, bananas, True)
    for colisao in colisoes:
        jogador.pontuacao += 10
    
    # Desenhar
    tela.fill(PRETO)
    todos_sprites.draw(tela)
    
    # Mostrar pontuação
    texto_pontuacao = fonte.render(f"Bananas: {jogador.pontuacao}", True, BRANCO)
    tela.blit(texto_pontuacao, (10, 10))
    
    # Atualizar tela
    pygame.display.flip()

pygame.quit()
sys.exit()
