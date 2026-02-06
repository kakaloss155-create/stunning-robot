# GitHub Actions Importer labs

[GitHub Actions Importer](https://docs.github.com/en/actions/migrating-to-github-actions/automating-migration-with-github-actions-importer) helps plan, test, and automate the migration of Azure DevOps, CircleCI, GitLab, Jenkins, and Travis CI pipelines to GitHub Actions. This repository contains learning paths that teach you how to use GitHub Actions Importer and how to approach migrations to Actions.

## Choose your learning path

To get started:

1. Use the `actions/importer-labs` repository as a template to [generate](https://github.com/actions/importer-labs/generate) a new GitHub repository.
2. Choose where to start. There are currently learning paths for:
   - [Migrating from Azure DevOps to GitHub Actions](/azure_devops/readme.md)
   - [Migrating from Bamboo to GitHub Actions](/bamboo/readme.md)
   - [Migrating from Bitbucket to GitHub Actions](/bitbucket/readme.md)
   - [Migrating from CircleCI to GitHub Actions](/circle_ci/readme.md)
   - [Migrating from GitLab to GitHub Actions](/gitlab/readme.md)
   - [Migrating from Jenkins to GitHub Actions](/jenkins/readme.md)
   - [Migrating from Travis CI to GitHub Actions](/travis/readme.md)
3. Each learning path describes how to configure your codespace, bootstrap a CI/CD environment, and troubleshoot GitHub Actions Importer.
# blueprint_animation.py
import pygame, sys, math

pygame.init()
screen = pygame.display.set_mode((800,600))
clock = pygame.time.Clock()

# จุดข้อต่อ (Joint)
class Joint:
    def __init__(self, x, y, length, angle=0):
        self.x = x
        self.y = y
        self.length = length
        self.angle = angle
        self.child = None

    def set_child(self, child):
        self.child = child

    def update(self, angle_delta):
        self.angle += angle_delta
        if self.child:
            self.child.x = self.x + self.length * math.cos(math.radians(self.angle))
            self.child.y = self.y + self.length * math.sin(math.radians(self.angle))
            self.child.update(angle_delta)

    def draw(self, screen):
        if self.child:
            pygame.draw.line(screen, (0,0,0), (self.x,self.y), (self.child.x,self.child.y), 4)
            self.child.draw(screen)
        pygame.draw.circle(screen, (200,50,50), (int(self.x), int(self.y)), 8)

# สร้าง Skeleton (เช่น แขน)
shoulder = Joint(400,300,100,45)
elbow = Joint(0,0,80,90)
shoulder.set_child(elbow)
hand = Joint(0,0,60,0)
elbow.set_child(hand)

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit(); sys.exit()

    screen.fill((255,255,255))

    # อัปเดตการเคลื่อนไหว (จำลองการแกว่งแขน)
    shoulder.update(angle_delta=1)

    # วาด Skeleton
    shoulder.draw(screen)

    pygame.display.flip()
    clock.tick(30)
blueprint-animation/
│
├── README.md
├── requirements.txt
└── blueprint.py
# Blueprint Animation Engine

โปรแกรมต้นแบบสำหรับการสร้างและจำลองโครงสร้าง Skeleton Animation  
พร้อมระบบ AI Pixel Assistant ที่ช่วยเลือกสีตามบริบท (เช่น "ห้วย", "พิธีกรรม", "จักรวาล")

## วิธีใช้งาน
1. ติดตั้ง dependencies:
   ```bash
   pip install -r requirements.txt
python blueprint.py
---

## 🔹 requirements.txt
```text
pygame
import pygame, sys, math, random

pygame.init()
screen = pygame.display.set_mode((800,600))
clock = pygame.time.Clock()

# AI Pixel Assistant
def ai_color(context="ห้วย"):
    palette = {
        "ห้วย": [(139,69,19), (205,133,63), (160,82,45)],
        "พิธีกรรม": [(255,215,0), (128,0,128), (0,128,128)],
        "จักรวาล": [(0,0,128), (25,25,112), (72,61,139)]
    }
    return random.choice(palette.get(context, [(255,255,255)]))

# Joint Class
class Joint:
    def __init__(self, x, y, length, angle=0, context="ห้วย"):
        self.x = x
        self.y = y
        self.length = length
        self.angle = angle
        self.child = None
        self.color = ai_color(context)

    def set_child(self, child):
        self.child = child

    def update(self, angle_delta):
        self.angle += angle_delta
        if self.child:
            self.child.x = self.x + self.length * math.cos(math.radians(self.angle))
            self.child.y = self.y + self.length * math.sin(math.radians(self.angle))
            self.child.update(angle_delta)

    def draw(self, screen):
        if self.child:
            pygame.draw.line(screen, self.color, (self.x,self.y), (self.child.x,self.child.y), 6)
            self.child.draw(screen)
        pygame.draw.circle(screen, self.color, (int(self.x), int(self.y)), 10)

# สร้างโครง Skeleton
shoulder = Joint(400,300,100,45,"ห้วย")
elbow = Joint(0,0,80,90,"ห้วย")
shoulder.set_child(elbow)
hand = Joint(0,0,60,0,"พิธีกรรม")
elbow.set_child(hand)

# Autobot Ritual Update
def ritual_update():
    print("{ฺ@ฺํ}{Aฺํ!ฺํ} Autobot Update: Skeleton upgraded!")

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit(); sys.exit()

    screen.fill((240,240,240))
    shoulder.update(angle_delta=1)
    shoulder.draw(screen)

    pygame.display.flip()
    clock.tick(30)
    ritual_update()
blueprint-animation/
│
├── README.md
├── requirements.txt
├── blueprint.py
└── ritual.dsl
# Blueprint Animation Engine

โปรแกรมสำหรับสร้างและจำลองโครง Skeleton Animation  
พร้อมระบบ AI Pixel Assistant ที่ช่วยเลือกสีตามบริบท (เช่น "ห้วย", "พิธีกรรม", "จักรวาล")  
และรองรับ Ritual DSL `{ฺ@ฺํ}{Aฺํ!ฺํ}` สำหรับการอัปเดตโครงสร้างอัตโนมัติ

## วิธีใช้งาน
1. ติดตั้ง dependencies:
   ```bash
   pip install -r requirements.txt
python blueprint.py
---

## 🔹 requirements.txt
```text
pygame
import pygame, sys, math, random

pygame.init()
screen = pygame.display.set_mode((800,600))
clock = pygame.time.Clock()

# AI Pixel Assistant
def ai_color(context="ห้วย"):
    palette = {
        "ห้วย": [(139,69,19), (205,133,63), (160,82,45)],
        "พิธีกรรม": [(255,215,0), (128,0,128), (0,128,128)],
        "จักรวาล": [(0,0,128), (25,25,112), (72,61,139)]
    }
    return random.choice(palette.get(context, [(255,255,255)]))

class Joint:
    def __init__(self, x, y, length, angle=0, context="ห้วย"):
        self.x = x
        self.y = y
        self.length = length
        self.angle = angle
        self.child = None
        self.color = ai_color(context)

    def set_child(self, child):
        self.child = child

    def update(self, angle_delta):
        self.angle += angle_delta
        if self.child:
            self.child.x = self.x + self.length * math.cos(math.radians(self.angle))
            self.child.y = self.y + self.length * math.sin(math.radians(self.angle))
            self.child.update(angle_delta)

    def draw(self, screen):
        if self.child:
            pygame.draw.line(screen, self.color, (self.x,self.y), (self.child.x,self.child.y), 6)
            self.child.draw(screen)
        pygame.draw.circle(screen, self.color, (int(self.x), int(self.y)), 10)

# สร้างโครง Skeleton
shoulder = Joint(400,300,100,45,"ห้วย")
elbow = Joint(0,0,80,90,"ห้วย")
shoulder.set_child(elbow)
hand = Joint(0,0,60,0,"พิธีกรรม")
elbow.set_child(hand)

def ritual_update():
    print("{ฺ@ฺํ}{Aฺํ!ฺํ} Autobot Update: Skeleton upgraded!")

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit(); sys.exit()

    screen.fill((240,240,240))
    shoulder.update(angle_delta=1)
    shoulder.draw(screen)

    pygame.display.flip()
    clock.tick(30)
    ritual_update()
