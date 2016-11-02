---
title: Dimme Lysdiode
level: 2
author: Mats Reime
---

# Introduksjon {.intro}

La oss se på å få ett display til å telle.

# Steg 1: Finn frem utstyr {.activity}

## Til denne oppgaven trenger du {.check}

+ 1 Arduino Uno
+ 1 breadboard
+ 2 motstander 10k Ohm (Fargekode: brun-svart-gul-gull)
+ 2 motstander 220 Ohm (Fargekode: rød-rød-brun-gull)
+ 2 knappbrytere
+ 2 lysdioder (du velger farge)
+ x antall ledninger


![kopling](kopling.png)

# Steg 2: Utforskning {.activity}

´´´cpp

int led1 = 5;
int led2 = 6;

int knapp1 = 2;
int knapp2 = 3;

int PWM_1 = 0;
int PWM_2 = 255;

void setup() {

  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(knapp1, INPUT);
  pinMode(knapp2, INPUT);
  Serial.begin(9600);
}

void loop() {
  analogWrite(led1, PWM_1);
  analogWrite(led2, PWM_2);

  //KNAPP NEDE
  while (digitalRead(knapp1) == HIGH)
  {
    if (PWM_1 >= 255) {
      while (digitalRead(knapp1) == HIGH) {
        digitalWrite(led2, LOW);
        digitalWrite(led1, HIGH);
        delay(100);
        digitalWrite(led1, LOW);
        delay(100);
      }
    }
    PWM_1 = PWM_1 + 5;
    PWM_2 = PWM_2 - 5;
    if (PWM_1 >= 255)PWM_1 = 255;
    if (PWM_2 <= 0) PWM_2 = 0;
    delay(100);
    analogWrite(led1, PWM_1);
    analogWrite(led2, PWM_2);
    Serial.println(PWM_1);
    Serial.println(PWM_2);

  }

  //KNAPP OPPE
  while (digitalRead(knapp2) == HIGH)
  {
    if (PWM_2 >= 255) {
      while (digitalRead(knapp2) == HIGH) {
        digitalWrite(led1, LOW);
        digitalWrite(led2, HIGH);
        delay(100);
        digitalWrite(led2, LOW);
        delay(100);
      }
    }
    PWM_2 = PWM_2 + 5;
    PWM_1 = PWM_1 - 5;
    if (PWM_2 >= 255)PWM_2 = 255;
    if (PWM_1 <= 0) PWM_1 = 0;
    delay(100);
    analogWrite(led2, PWM_2);
    analogWrite(led1, PWM_1);
    Serial.println(PWM_1);
    Serial.println(PWM_2);
  }
}

´´´
