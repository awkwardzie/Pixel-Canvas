import pygame
import sys

# Canvas Selection Before Pygame Starts
print("Choose your canvas size:")
print("1 = Square")
print("2 = Landscape")
print("3 = Portrait")

choice = input("Enter your choice (1, 2, or 3): ")

if choice == "1":
    WIDTH = 600
    HEIGHT = 600
    canvas_type = "Square"

elif choice == "2":
    WIDTH = 800
    HEIGHT = 500
    canvas_type = "Landscape"

elif choice == "3":
    WIDTH = 500
    HEIGHT = 800
    canvas_type = "Portrait"

else:
    print("Invalid choice. Defaulting to Square canvas.")
    WIDTH = 600
    HEIGHT = 600
    canvas_type = "Square"

# Sidebar Settings
SIDEBAR_WIDTH = 120
DRAW_WIDTH = WIDTH - SIDEBAR_WIDTH

# Grid Settings
# Start with preferred size
PREFERRED_PIXEL_SIZE = 60

# Adjust pixel size so grid fits perfectly
PIXEL_SIZE = min(
    WIDTH // (WIDTH // PREFERRED_PIXEL_SIZE),
    HEIGHT // (HEIGHT // PREFERRED_PIXEL_SIZE)
)

# Safety check if window is smaller than preferred size
if PIXEL_SIZE <= 0:
    PIXEL_SIZE = 60

# Number of rows and columns
ROWS = HEIGHT // PIXEL_SIZE
COLS = DRAW_WIDTH // PIXEL_SIZE

# Initialize Pygame
pygame.init()

screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption(f"Pixel Canvas - {canvas_type}")

# Colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 0, 0)
ORANGE = (255, 165, 0)
YELLOW = (255, 255, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)
PURPLE = (128, 0, 128)
PINK = (255, 105, 180)
BROWN = (139, 69, 19)
GRAY = (120, 120, 120)
DARK_GRAY = (40, 40, 40)

# Click palette colors
PALETTE_COLORS = [
    BLACK,
    WHITE,
    RED,
    ORANGE,
    YELLOW,
    GREEN,
    BLUE,
    PURPLE,
    PINK,
    BROWN
]

# Default selected color
selected_color = WHITE

# Grid Data Storage
# Store the color of each square
grid = []

for row in range(ROWS):
    grid_row = []
    for col in range(COLS):
        grid_row.append(BLACK)
    grid.append(grid_row)

# Function to Clear Canvas
def clear_canvas():
    for row in range(ROWS):
        for col in range(COLS):
            grid[row][col] = BLACK

# Function to Draw Grid
def draw_grid():
    for row in range(ROWS):
        for col in range(COLS):
            x = col * PIXEL_SIZE
            y = row * PIXEL_SIZE

            rect = pygame.Rect(x, y, PIXEL_SIZE, PIXEL_SIZE)

            pygame.draw.rect(screen, grid[row][col], rect)
            pygame.draw.rect(screen, GRAY, rect, 2)

# Function to Draw Sidebar
def draw_sidebar():
    # Sidebar background
    sidebar_rect = pygame.Rect(DRAW_WIDTH, 0, SIDEBAR_WIDTH, HEIGHT)
    pygame.draw.rect(screen, DARK_GRAY, sidebar_rect)

    box_size = 35
    padding = 10

    for i, color in enumerate(PALETTE_COLORS):
        x = DRAW_WIDTH + 40
        y = padding + i * (box_size + padding)

        color_rect = pygame.Rect(x, y, box_size, box_size)

        pygame.draw.rect(screen, color, color_rect)
        pygame.draw.rect(screen, WHITE, color_rect, 2)

        # Highlight selected color
        if color == selected_color:
            pygame.draw.rect(screen, GRAY, color_rect, 5)

# Function to Select Color
def select_color(mouse_x, mouse_y):
    global selected_color

    box_size = 35
    padding = 10

    for i, color in enumerate(PALETTE_COLORS):
        x = DRAW_WIDTH + 40
        y = padding + i * (box_size + padding)

        color_rect = pygame.Rect(x, y, box_size, box_size)

        if color_rect.collidepoint(mouse_x, mouse_y):
            selected_color = color

# Function to Paint Square
def paint_square(mouse_x, mouse_y):
    if mouse_x >= DRAW_WIDTH:
        return

    col = mouse_x // PIXEL_SIZE
    row = mouse_y // PIXEL_SIZE

    if row < ROWS and col < COLS:
        grid[row][col] = selected_color

# Main Game Loop
running = True
mouse_held = False

print("Press C to clear the canvas")

while running:
    for event in pygame.event.get():

        # Close window using X button
        if event.type == pygame.QUIT:
            running = False

        # Press ESC key to close window
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_ESCAPE:
                running = False

            # C clears canvas
            if event.key == pygame.K_c:
                clear_canvas()

        # Mouse pressed
        if event.type == pygame.MOUSEBUTTONDOWN:
            mouse_held = True

            mouse_x, mouse_y = pygame.mouse.get_pos()

            # Clicking sidebar selects color
            if mouse_x >= DRAW_WIDTH:
                select_color(mouse_x, mouse_y)

            # Clicking canvas paints
            else:
                paint_square(mouse_x, mouse_y)
        # Mouse released
        if event.type == pygame.MOUSEBUTTONUP:
            mouse_held = False

        # Drag painting
        if event.type == pygame.MOUSEMOTION and mouse_held:
            mouse_x, mouse_y = pygame.mouse.get_pos()

            if mouse_x < DRAW_WIDTH:
                paint_square(mouse_x, mouse_y)


  # Background Color
    screen.fill(BLACK)
    draw_grid()
    draw_sidebar()
    pygame.display.update()

# Close Program
pygame.quit()
sys.exit()