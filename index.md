# Mystery of Circles

An OpenGl application with GLUT library which you can press your mouse, hold & move it to see the mystery.

***

## Circle

It's a class for creating circles & draw them on the screen.
Its ***Circle::draw()*** function will draw a circle with three random numbers as red, green & blue for setting the each circle color.
Also, we create a loop of vertex with its own properties.
<br>
**Circle**
```C
class Circle
{
public:
	float x, y, r, alpha;
	Circle(float _x = 0.0, float _y = 0.0, float _r = 10.0): x(_x), y(_y), r(_r), alpha(1.0) {};
	void draw();
};

```
<br>

**Line Loop** 
```c
glBegin(GL_LINE_LOOP);
	for (float i = 0.0; i < 2 * 3.14; i += 3.14 / 18)
	{
		glVertex2f(this->x + this->r * sin(i), this->y + this->r * cos(i));
	}
	glEnd();
```

***

## Draw & Global Properties

We have a function ***void Draw()*** which draw the circles & delete them from the ***vector*** . Also, we enable the some OpenGL properties like **GL_ALPHA**, **GL_BLEND** to enable alpha & blend features.
<br>

**Global Properties**
```c
vector<Circle> circ;

float WinWid = 600.0;
float WinHei = 600.0;
float X = 0.0, Y = 0.0;
bool down = false;
```
<br>

**Draw()**
```c

	glClear(GL_COLOR_BUFFER_BIT);
	glEnable(GL_ALPHA);
	glEnable(GL_BLEND);
	glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
	vector<Circle>::iterator i = circ.begin();
	while (i != circ.end())
	{
		i->draw();
		if (i->alpha <= 0.05f)
			i = circ.erase(i);
		else
			++i;
	}
	glDisable(GL_BLEND);
	glDisable(GL_ALPHA);
	glutSwapBuffers();
```
***

## Timer & Timer2 Functions
***Timer***  function increment the radius of the circles & divide the **alpha** property by 1.05 .

***Timer2*** function create circle with X, Y and Radius then push it back to the vector.

***

## Pressed Functions
***MousePressed()*** function is used for getting the coordinates of screen to create circles.

***MouseMovePressed*** function is used for getting the coordinates of screen if mouse is still pressed.

```c
void MousePressed(int button, int state, int ax, int ay)
{
	down = button == GLUT_LEFT_BUTTON && state == GLUT_LEFT;
	if (down)
	{
		X = ax - WinWid / 2;
		Y = ay - WinHei / 2;
	}
}

void MouseMovePressed(int ax, int ay)
{
	if (down)
	{
		X = ax - WinWid / 2;
		Y = ay - WinHei / 2;
	}
}
```
