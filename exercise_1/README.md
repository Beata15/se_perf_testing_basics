# Exercise 1

1. Wystartuj instancję ghosta:

   ```
   $ sudo docker run -d --name my-ghost -e url=http://localhost:3001 -p 3001:2368 ghost
   ```

   Open in browser: http://127.0.0.1:3001

2. W osobnym terminalu wyświetlmy logi:

   ```
   $ sudo docker logs my-ghost -f
   ```

3. Czas, na testy. Zacznijmy, klasycznie, z Siege ([homepage](https://www.joedog.org/siege-home/)):

   ```
   $ siege -t30s -c2 –header='X-USER-AGENT:android_4.4.4' 127.0.0.1:3001
   ``` 

   ```
   $ siege -t30s -c100 –header='X-USER-AGENT:android_4.4.4' 127.0.0.1:3001
   ```

   ```
   $ siege -t30s -c255 127.0.0.1:3001
   ```

   Co się zmieniło?

4. Czas na bardziej złożone narzęcie - locust. Przejrzyj: `locustfile.py`.

5. Teraz czas na jego uruchominie:

   ```
   # najpierw czas na zainstalowanie wymaganych bibliotek
   $ python3 -m venv .venv
   $ pip install locust

   # czas zacząć test
   $ locust -f locustfile.py
   ```
   
   Otwórz: http://127.0.0.1:8089

6. Czas wyłączyć nasz kontener z blogiem:

   ```
   $ sudo docker stop my-ghost
   $ sudo docker rm my-ghost
   # powinieneś zobaczyć pustą listę
   $ sudo docker ps
   ```
