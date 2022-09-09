![photo_2022-09-09_20-36-04](https://user-images.githubusercontent.com/110935510/189412450-4f3ce97c-8727-45bb-be68-347155a74a9e.png)

## Тестирование API с использованием Rest-Assured 🌐
В этом проекте я хочу поделиться своим опытом в написании API тестов на языке Java. 

Для тестирования использовалось API - https://reqres.in 

### Был составлен следующий чек-лист:
- Проверка статус-кода [GET]
- Создание нового пользователя [POST]
- Успешная регистрация [POST]
- Регистрация без пароля (запрет) [POST]
- Получение конкретного пользователя из списка по e-mail [GET]
- E-mail заканчивается на @reqres.in [GET]
- Изменение пользователя [PATCH]

### Maven-зависимости в проекте:
![image](https://user-images.githubusercontent.com/110935510/189408867-8b55cd72-5e57-45be-b59a-d48a983a2f73.png)

#### В проекте имеется 3 класса:
![image](https://user-images.githubusercontent.com/110935510/189409826-f8dd647f-db47-4cef-a514-a01c0d1a2e5b.png)

- ApiTests - основной класс, в котором реализованы все проверки.
- RequestBodies и UsersPojo - хелпер-классы, которые используются для вынесения в них объёмных частей кода (например передаваемых тел запросов).
#### В класс UsersPojo помещаются передаваемые в ответе данные для дальнейшей их сортировки через stream().filter(). 

### Немного слов про JUnit-аннотации: 

Перед объявлением класса используется аннотация @TestMethodOrder(MethodOrderer.DisplayName.class) для того, чтобы упорядочить выполнение тесто один за другим, в строгой последовательности.

![image](https://user-images.githubusercontent.com/110935510/189411023-dc2ba880-fda2-4043-b489-8e17a7f43a55.png)

Аннотация @Test проставляется перед каждым тестовым методом, а @DisplayName задаёт удобочитаемое название для методов в общем пулле тестов.

### Пример кода для осуществления проверки "Создание нового пользователя"
В этом тесте мы будем использовать http-метод POST и передавать тело запроса.
Предварительно это самое тело запроса я вынес в переменную типа String в класс RequestBodies, а в моём главном классе (ApiTests) я просто экстендю класс с телами запросов и использую созданную переменную.

![image](https://user-images.githubusercontent.com/110935510/189415073-59cbc93e-4336-493a-83e2-b11f5bdf7767.png)

Создаём объект response и помещаем в него наш ответ с помощью .extract().response()

После выполнения метода POST ответ от сервера хранится в нашем объекте response, который нам нужен для осуществления проверок.

Прописываем ассерты на соответствие значений в полях name и job: 

![image](https://user-images.githubusercontent.com/110935510/189414276-2af9bba9-9e69-45cc-a7d2-c0fe8a2c7a30.png)


### Результаты проверок:
![image](https://user-images.githubusercontent.com/110935510/189410163-d4484fb3-ce3d-4738-85c8-efb4b8d5f38f.png)





