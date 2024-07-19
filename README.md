
#include <stdio.h>
#include <math.h>

#define PI 3.14159265358979323846

void draw_star(int size) {
    int width = 2 * size + 1;
    int height = size + 1;
    char canvas[height][width];

    // Initialize canvas with spaces
    for (int i = 0; i < height; i++) {
        for (int j = 0; j < width; j++) {
            canvas[i][j] = ' ';
        }
    }

    // Draw the star
    for (int i = 0; i < 5; i++) {
        double angle1 = i * 2.0 * PI / 5.0;
        double angle2 = (i * 2.0 + 2.0) * PI / 5.0;
        
        int x1 = size + (int)(size * sin(angle1));
        int y1 = size - (int)(size * cos(angle1));
        int x2 = size + (int)(size * sin(angle2));
        int y2 = size - (int)(size * cos(angle2));
        
        int dx = abs(x2 - x1), sx = x1 < x2 ? 1 : -1;
        int dy = abs(y2 - y1), sy = y1 < y2 ? 1 : -1; 
        int err = (dx > dy ? dx : -dy) / 2, e2;
        
        while (1) {
            if (x1 >= 0 && x1 < width && y1 >= 0 && y1 < height) {
                canvas[y1][x1] = '*';
            }
            if (x1 == x2 && y1 == y2) break;
            e2 = err;
            if (e2 > -dx) { err -= dy; x1 += sx; }
            if (e2 < dy) { err += dx; y1 += sy; }
        }
    }

    // Print the canvas
    for (int i = 0; i < height; i++) {
        for (int j = 0; j < width; j++) {
            putchar(canvas[i][j]);
        }
        putchar('\n');
    }
}

int main() {
    int size = 10;
    draw_star(size);
    return 0;
}
