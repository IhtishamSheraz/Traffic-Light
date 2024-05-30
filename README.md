# Traffic-Light
#include <SFML/Graphics.hpp>
#include <iostream>

using namespace sf;

const int RED = 0;
const int YELLOW = 1;
const int GREEN = 2;

int main()
{
    RenderWindow window(VideoMode(300, 600), "Traffic Signal");

    CircleShape redLight(50.f);
    redLight.setFillColor(Color::Red);
    redLight.setPosition(100.f, 50.f);

    CircleShape yellowLight(50.f);
    yellowLight.setFillColor(Color(128, 128, 0)); // Dark yellow color
    yellowLight.setPosition(100.f, 250.f);

    CircleShape greenLight(50.f);
    greenLight.setFillColor(Color::Green);
    greenLight.setPosition(100.f, 450.f);

    int currentState = RED;
    Clock clock;
    Time elapsed;

    while (window.isOpen())
    {
        Event event;
        while (window.pollEvent(event))
        {
            if (event.type == Event::Closed)
                window.close();
        }

        elapsed = clock.getElapsedTime();
        if (elapsed.asSeconds() > 5)
        {
            clock.restart();
            if (currentState == RED)
                currentState = YELLOW;
            else if (currentState == YELLOW)
                currentState = GREEN;
            else if (currentState == GREEN)
                currentState = RED;
        }

        // Set lights based on current state
        if (currentState == RED)
        {
            redLight.setFillColor(Color::Red);
            yellowLight.setFillColor(Color(128, 128, 0));
            greenLight.setFillColor(Color(0, 128, 0));
        }
        else if (currentState == YELLOW)
        {
            redLight.setFillColor(Color(128, 0, 0));
            yellowLight.setFillColor(Color::Yellow);
            greenLight.setFillColor(Color(0, 128, 0));
        }
        else if (currentState == GREEN)
        {
            redLight.setFillColor(Color(128, 0, 0));
            yellowLight.setFillColor(Color(128, 128, 0));
            greenLight.setFillColor(Color::Green);
        }

        window.clear(Color::Black);
        window.draw(redLight);
        window.draw(yellowLight);
        window.draw(greenLight);
        window.display();
    }

    return 0;
}
