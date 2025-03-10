import pygame
import time

# 初始化 Pygame
pygame.init()

# 设置窗口大小
width, height = 800, 600
screen = pygame.display.set_mode((width, height))
pygame.display.set_caption("动画手账")

# 加载背景图片
background = pygame.image.load("background.jpg")
background = pygame.transform.scale(background, (width, height))

# 定义字体
font = pygame.font.Font(None, 36)

# 定义文本内容
chinese_text = "明月"
pinyin_text = "míng yuè"
english_text = "Bright moon"
phrase_text = "明月高悬"
sentence_text = "明月照高楼，流光正徘徊。"
oral_text = "今晚的明月真美啊！"

texts = [chinese_text, pinyin_text, english_text, phrase_text, sentence_text, oral_text]

# 主循环
running = True
index = 0
start_time = time.time()
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # 绘制背景
    screen.blit(background, (0, 0))

    # 逐行显示文本
    if index < len(texts):
        elapsed_time = time.time() - start_time
        if elapsed_time > 3:  # 每 3 秒显示一行新文本
            index += 1
            start_time = time.time()

        for i in range(index + 1):
            text = texts[i]
            text_surface = font.render(text, True, (255, 255, 255))
            text_rect = text_surface.get_rect(center=(width // 2, 50 + i * 80))
            screen.blit(text_surface, text_rect)

    pygame.display.flip()

# 退出 Pygame
pygame.quit()


