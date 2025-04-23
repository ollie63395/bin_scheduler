#include <Wire.h>
#include <LiquidCrystal.h>
#include <RTClib.h>

// RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
RTC_DS1307 rtc;

const char* daysOfWeek[] = {"Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"};

int getWeekNumber(DateTime now) {
  DateTime startOfYear(2025, 3, 12, 0, 0, 0);

  // Calculate days passed
  TimeSpan elapsed = now - startOfYear;
  int weekNumber = (elapsed.days() / 7) + 1;

  return weekNumber;
}

void setup() {
  Serial.begin(9600);
  lcd.begin(16, 2);
  rtc.begin();

  if (!rtc.isrunning()) {
    // Uncomment this line to set the time the first time you upload
    rtc.adjust(DateTime(F(__DATE__), F(__TIME__)));
  }

  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
}

void loop() {
  // nothing here
  DateTime now = rtc.now();
  int weekNumber = getWeekNumber(now);

  // Determine bin type
  const char* bin = (weekNumber % 2 == 0) ? "Y" : "R";

  // Determine person (customize this!)
  const char* people[] = {"Emmy", "Hannah", "Ollie"};
  const char* person = people[weekNumber % 3];

  lcd.setCursor(0, 0);
  lcd.print(now.day());
  lcd.print("/");
  lcd.print(now.month());
  lcd.print("/");
  lcd.print(now.year());
  lcd.print(", ");
  lcd.print(daysOfWeek[now.dayOfTheWeek()]);

  lcd.setCursor(0, 1);
  lcd.print(person);
  lcd.print(" (");
  lcd.print(bin);
  lcd.print(")");

  if (weekNumber % 2 == 0) {
    // Yellow bin week
    digitalWrite(7, LOW);
    digitalWrite(8, HIGH);
  } else {
    // Red bin week
    digitalWrite(7, HIGH);
    digitalWrite(8, LOW);
  }
  
  delay(5000);
}
