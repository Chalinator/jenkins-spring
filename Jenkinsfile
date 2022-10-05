pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
        // w konfiguracji jenkinsa dodaje w globalnych narzędziach mavena jako nazwę M3, od teraz mogę uzywać tego aliasu
    }

    stages {
        stage('Build') {
            steps { // 1 etap: budowanie aplikacji
            sh "mvn clean compile" // komenda mejvnowa służy do przebudowania projektu, wcześniej usunięcia wszystkiego z katalogu roboczego
            }
        stage('Test') { // przetestuj
            steps {
            sh "mvn test"
            }
        }
        stage('Deploy') {
            steps { // niżej dodany clean, żeby to był czysty katalog
            sh "mvn clean heroku:deploy" // komenda wynika z dokumentacji technicznej heroku, kopiujemy resztę do poma,
            // w komendzie z <processTypes> zmieniamy na wzór java -jar i nazwa aplikacji. Jest to polecenie, które ma się wykonać w momencie
            // uruchomienia. Żeby nie pisać na sztywno nazwy aplikacji, można się posłużyć zmienną. Domyślnie aplikacja zbuduje się
            // w katalogu target. Po dolarze odwołujemy się do zmiennej, która będzie przechowywać nazwę aplikacji.
            // Trzeba jeszcze dodać flagę, która będzie wzskazywać serwerowi, na jakim porcie ma być uruchomione (maping),
            // żeby aplikacja na heroku nie uruchamiała się na konkretnym porcie, tylko bezpośrednio pod danym adresem.
            // w porcie można wpisć adres na sztywno, ale po dolarze profesjonalnie jest użyć PORT, który przekaże info o użytym porcie
            // Czyli zostało zdefionowane wszystko co ma się wykonać w ramach heroku, aplikacja będzie starała się zbudować i wzdrożyć
            }
        }
    }
}
