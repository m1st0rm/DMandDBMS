<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
</head>
<body>
    <h1>Тема: Электронная библиотека</h1>
    <p>ФИО: Богомолов Михаил Алесандрович</p>
    <p>Номер группы: 153502</p>
    <h2>Функциональные требования</h2>
    <ol>
        <li>
            <h3>Регистрация и аутентификация:</h3>
            <ul>
                <li>Пользователи могут зарегистрировать аккаунт.</li>
                <li>Пользователи могут войти в систему с помощью своих учетных данных (Email и пароль).</li>
            </ul>
        </li>
        <li>
            <h3>Управление профилем пользователя:</h3>
            <ul>
                <li>Пользователи могут обновлять информацию о своем профиле (например, имя, фамилия, пароль).</li>
                <li>Пользователи могут просматривать свой профиль и историю действий.</li>
            </ul>
        </li>
        <li>
            <h3>Поиск и просмотр книг:</h3>
            <ul>
                <li>Пользователи могут искать книги по различным критериям (название, автор, жанр и т.д.).</li>
                <li>Пользователи могут просматривать детали о каждой книге, включая описание, автора и отзывы.</li>
            </ul>
        </li>
        <li>
            <h3>Управление библиотекой:</h3>
            <ul>
                <li>Пользователи могут добавлять книги в избранное.</li>
                <li>Пользователи могут оставлять отзывы и оценки для книг.</li>
                <li>Пользователи могут просматривать свои избранные книги и отзывы.</li>
            </ul>
        </li>
        <li>
            <h3>Администрирование:</h3>
            <ul>
                <li>Администраторы могут управлять пользователями (блокировка, удаление).</li>
                <li>Администраторы могут создавать и управлять ролями пользователей.</li>
                <li>Администраторы могут добавлять и редактировать информацию о книгах.</li>
                <li>Администраторы могут генерировать отчеты о популярности книг.</li>
            </ul>
        </li>
        <li>
            <h3>Выдача и возврат книг:</h3>
            <ul>
                <li>Пользователи могут брать книги в аренду и устанавливать сроки возврата.</li>
                <li>Система отслеживает сроки возврата и предоставляет уведомления пользователям.</li>
                <li>Пользователи могут возвращать книги и обновлять их статус в системе.</li>
            </ul>
        </li>
        <li>
            <h3>Статистика и отчеты:</h3>
            <ul>
                <li>Система предоставляет статистику о популярности книг, оценках и отзывах.</li>
                <li>Администраторы могут генерировать отчеты о деятельности в системе.</li>
            </ul>
        </li>
        <li>
            <h3>Система управления ролями:</h3>
            <ul>
                <li>Роли пользователей (например, обычные пользователи, администраторы) управляют доступом к функциям.</li>
            </ul>
        </li>
        <li>
            <h3>Безопасность:</h3>
            <ul>
                <li>Авторизация и аутентификация пользователей.</li>
            </ul>
        </li>
        <li>
            <h3>Уведомления:</h3>
            <ul>
                <li>Система предоставляет уведомления пользователям о событиях (например, о ближайших сроках возврата книг).</li>
            </ul>
        </li>
        <li>
            <h3>Многопользовательская поддержка:</h3>
            <ul>
                <li>Система должна поддерживать работу множества пользователей одновременно без конфликтов.</li>
            </ul>
        </li>
    </ol>
    <h2>Описание сущностей БД</h2>
    <h3>Сущность "Пользователь" (User)</h3>
    <ul>
        <li>ID пользователя (INT, PK) - связь один к многим с UserActionLog, связь один к многим с Review, связь один к многим с Favorite</li>
        <li>Имя (VARCHAR)</li>
        <li>Фамилия (VARCHAR)</li>
        <li>Email (VARCHAR)</li>
        <li>Пароль (VARCHAR)</li>
        <li>Дата регистрации (DATE)</li>
        <li>ID библиотечной карты (INT, FK) - Связь один к одному с LibraryCard</li>
        <li>ID роли (INT, FK) - Связь многие к одному с Role</li>
    </ul>
    <h3>Сущность "Избранное" (Favorite)</h3>
    <ul>
        <li>ID записи (INT, PK)</li>
        <li>ID пользователя (INT, FK) - Связь многие к одному с User</li>
        <li>ID книги (INT, FK) - Связь многие к одному с Book</li>
    </ul>
    <h3>Сущность "Книга" (Book)</h3>
    <ul>
        <li>ID книги (INT, PK)</li> - Связь многие к многим с Author через таблицу AuthorBook, связь один к многим с BookCopy, связь один к многим с Review, связть один к многим с BookReport, связь один к многим с Favorite</li>
        <li>Название (VARCHAR)</li>
        <li>ID жанра (INT, FK) - Связь многие к одному с Genre</li>
        <li>ID издательства (INT, FK) - Связь многие к одному с Publisher</li>
        <li>ISBN (VARCHAR)</li>
        <li>Дата публикации (DATE)</li>
        <li>Описание (VARCHAR)</li>
    </ul>
    <h3>Сущность "Автор" (Author)</h3>
    <ul>
        <li>ID автора (INT, PK) - Связь многие к многим с Book через таблицу AuthorBook</li>
        <li>Имя (VARCHAR)</li>
        <li>Фамилия (VARCHAR)</li>
    </ul>
    <h3>Сущность "Автор-Книга" (AuthorBook) - промежуточная таблица между таблицами Book и Author</h3>
    <ul>
        <li>ID записи (INT, PK)</li>
        <li>ID автора (INT, FK) - Связь многие к одному с Author</li>
        <li>ID книги (INT, FK) - Связь многие к одному с Book</li>
    </ul>
    <h3>Сущность "Экземпляр книги" (BookCopy)</h3>
<ul>
    <li>ID экземпляра (INT, PK)</li>
    <li>ID книги (INT, FK) - Связь многие к одному с Book</li>
    <li>Состояние (VARCHAR)</li>
    <li>Дата возврата (DATE)</li>
    <li>Дата выдачи (DATE)</li>
</ul>
<h3>Сущность "Отзыв книги" (Review)</h3>
<ul>
    <li>ID отзыва (INT, PK)</li>
    <li>ID книги (INT, FK) - Связь многие к одному с Book</li>
    <li>ID пользователя (INT, FK) - Связь многие к одному с User</li>
    <li>Оценка (INT)</li>
    <li>Текст отзыва (TEXT)</li>
    <li>Дата отзыва (DATE)</li>
</ul>
<h3>Сущность "Отчет о популярности книги" (BookReport)</h3>
<ul>
    <li>ID отчета (INT, PK)</li>
    <li>ID книги (INT, FK) - Связь многие к одному с Book</li>
    <li>Количество просмотров (INT)</li>
    <li>Количество взятий книги (INT)</li>
    <li>Дата отчета (DATE)</li>
</ul>
<h3>Сущность "Жанр" (Genre)</h3>
<ul>
    <li>ID жанра (INT, PK) - Связь один к многим с Book</li>
    <li>Название жанра (VARCHAR)</li>
</ul>
<h3>Сущность "Издательство" (Publisher)</h3>
<ul>
    <li>ID издательства (INT, PK) - Связь один к многим с Book</li>
    <li>Название издательства (VARCHAR)</li>
</ul>
<h3>Сущность "Роль" (Role)</h3>
<ul>
    <li>ID роли (INT, PK) - Связь один ко многим с User</li>
    <li>Название роли (VARCHAR)</li>
</ul>
<h3>Сущность "Библиотечная карта" (LibraryCard)</h3>
<ul>
    <li>ID карты (INT, PK) - Связь один к одному с User</li>
    <li>Номер карты (VARCHAR)</li>
    <li>Дата выдачи (DATE)</li>
    <li>Срок действия (DATE)</li>
</ul>
<h3>Сущность "Журнал действий пользователя" (UserActionLog)</h3>
<ul>
    <li>ID записи (INT, PK)</li>
    <li>ID пользователя (INT, FK) - Связь один к одному с User </li>
    <li>Время и дата действия (DATETIME)</li>
    <li>Описание действия (VARCHAR)</li>
    <h2>Схема БД</h2>
    <img src = "https://github.com/m1st0rm/DM-and-DBMS/assets/94941809/c960e85b-73b8-474a-a067-7f0e6c067952">


</ul>
</body>
</html>
