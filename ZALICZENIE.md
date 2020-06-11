# Zaliczenie przedmiotu Wirtualizacja i przetwarzanie w chmurze

Autor: Joanna Margielewska (193863) (WZISS22412IS)

## Projekt, implementacja oraz wdrożenie aplikacji w środowisku AWS

Aplikacja generująca animację ze zdjęć, wdrożona z wykorzystaniem usług dostępnych w obrębie chmury AMAZON

### Wymagania dotyczące funkcjonalności

* Rejestracja użytkownika
* Autoryzacja dostępu do aplikacji
* Autoryzacja dostepu do zasobów
* Przechowywanie plików
* Integracja z wykorzystaniem HTTP
* Integracja z wykorzystaniem serwera kolejki
* Implementacja właściwej transformacji obrazów do video
* Notyfikacja użytkownika o zakończonym procesie

### Usługi wspomagające realizacje wymagań

* Amazon Cognito -> rejestracja oraz zarządzanie użytkownikami
* Cloud9 -> IDE
* Lambda -> tworzenie funkcji obsługi zdjęć, wysyłanie do kolejki, tworzenie animacji oraz notyfikacji na maila
* Simple Queue Service -> kolejka do animacji i notyfikacji
* Simple Email Service -> wysyłanie maila o stworzonej animacji
* S3 -> przechowywanie plików
* API Gateway -> API REST służące do integracji z funkcjami Lambda
* CloudWatch -> logowanie i pomoc w debugowaniu

### Charakterysytka modułów aplikacji
Wykorzystanie technologie, sposób integracji, opis funkcjonalności

* UI
    - javascript(webpack),css, html
    - integracja z S3 - przechowywanie,pobieranie plików
    - integracja z API Gateway(REST API) 
    - integracja z Amazon Cognito
    
* Transcoding
    - python
    - kolejka gdzie przechowywane są informacje o obrazach
    - integracja z API Gateway służące odbierania requestów z UI
    - integracja z S3 - przechowywanie,pobieranie plików
    - integracja z kolejką order animation, gdzie kolejka wywołuje funkcje create-slideshow tworzącą animacje 
    
* Notyfikacje
    - python
    - kolejka gdzie przechowywane są informacje o obrazach
    - integracja z kolejką orders-notifications, kolejka wywołuje funkcje notify, następnie wysyła notyfikacje na maila
    - integracja z Simple Email Service służąca do wysyłania maili

## Wady i zalety wdrożenia z wykorzystaniem chmury

+ mobilność i wygoda
+ niezależność od awarii sprzętu 
+ zawsze dostępne centrum obliczeniowe
+ elastyczność
+ skalowalność
+ optymalizacja kosztów firmowych

- bezpieczeństwo danych
- dostęp osób trzecich
- uzależnienie od internetu
- brak bezpośredniej/ograniczona kontrola na pewnymi usługami

## Wykorzystane uslugi

* Bucket ->  http://193863.s3-website-eu-west-1.amazonaws.com 193863
* API Gateway -> https://fwl9h5n50k.execute-api.eu-west-1.amazonaws.com/dev 193863-animation-api
* Lambda (zlecenie przygotowania animacji) -> 193863-order-animation
* Kolejka (zlecenia do wykonania) -> https://sqs.eu-west-1.amazonaws.com/881078108084/193863-order-animation 	193863-order-animation
* Lambda (transcoding) -> 193863-create-slideshow
* Kolejka (notyfikacje do wysłania) -> https://sqs.eu-west-1.amazonaws.com/881078108084/193863-orders-notifications 193863-orders-notifications
* Lambda (notyfikacja) -> 193863-notification

