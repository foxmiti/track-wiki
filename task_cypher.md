Очередное дело Шерлока Холмса закручивается вокруг странных пляшущих человечков — с первого взгляда, невинного детского рисунка.
Но Холмс догадывается, что это не просто детские каракули, а шифр! Шерлоку Холмсу удается расшифровать его и предотвратить убийство.
Для этого он воспользовался частотным анализом. Известно, что частота, с которой встречается буква в тексте на
определенном языке - это постоянная величина и используя эти сведения можно попытаться разгадать шифр.

Вам нужно построить гистограмму (таблицу частоты) для большого текста на английском языке.
На вход передается зашифрованный текст на английском языке [шифром подстановки] (https://ru.wikipedia.org/wiki/%D0%A8%D0%B8%D1%84%D1%80_%D0%BF%D0%BE%D0%B4%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B8).
Нужно написать программу, которая расшифрует входной текст используя гистограмму для английского языка.
Используйте для хранения гистограммы Map<K,V>, используйте встроенные алгоритмы сортировки.


На вход: 
- референсный текст на английском языке для составления гистограммы
- зашифрованный текст
На выход: 
- расшифрованный текст

Ссылки:
Частостный анализ https://ru.wikipedia.org/wiki/%D0%A7%D0%B0%D1%81%D1%82%D0%BE%D1%82%D0%BD%D1%8B%D0%B9_%D0%B0%D0%BD%D0%B0%D0%BB%D0%B8%D0%B7
Пляшущие человечки https://ru.wikipedia.org/wiki/%D0%9F%D0%BB%D1%8F%D1%88%D1%83%D1%89%D0%B8%D0%B5_%D1%87%D0%B5%D0%BB%D0%BE%D0%B2%D0%B5%D1%87%D0%BA%D0%B8

Задание **encoder** 
5 баллов

1) Генерация шифра
```
public class CypherUtil {

    public static final String SYMBOLS = "abcdefghijklmnopqrstuvwxyz";

    /**
     * Генерирует таблицу подстановки - то есть каждой буква алфавита ставится в соответствие другая буква
     * Не должно быть пересечений (a -> x, b -> x). Маппинг уникальный
     *
     * @return таблицу подстановки шифра
     */
    @NotNull
    public static Map<Character, Character> generateCypher() {
    }
}
```

2) Шифрование текста. Используем шифр из CypherUtil.generateCypher()

```
public class Encoder {

    /**
     * Метод шифрует символы текста в соответствие с таблицей
     * NOTE: Текст преводится в lower case!
     *
     * Если таблица: {a -> x, b -> y}
     * то текст aB -> xy, AB -> xy, ab -> xy
     *
     * @param cypherTable - таблица подстановки
     * @param text - исходный текст
     * @return зашифрованный текст
     */
    public String encode(@NotNull Map<Character, Character> cypherTable, @NotNull String text) {
        
    }
}
```

Задание **decoder**
10 баллов

3) Дешифрование

```
public class Decoder {

    // Расстояние между A-Z -> a-z
    public static final int SYMBOL_DIST = 32;

    private Map<Character, Character> cypher;

    /**
     * Конструктор строит гистограммы открытого домена и зашифрованного домена
     * Сортирует буквы в соответствие с их частотой и создает обратный шифр Map<Character, Character>
     *
     * @param domain - текст по кторому строим гистограмму языка
     */
    public Decoder(@NotNull String domain, @NotNull String encryptedDomain) {
        Map<Character, Integer> domainHist = createHist(domain);
        Map<Character, Integer> encryptedDomainHist = createHist(encryptedDomain);
        //...
        // Этот шифр используется в методе расшифровки
        this.cypher = ...;
    }

    public Map<Character, Character> getCypher() {
        return cypher;
    }

    /**
     * Применяет построенный шифр для расшифровки текста
     *
     * @param encoded зашифрованный текст
     * @return расшифровка
     */
    @NotNull
    public String decode(@NotNull String encoded) {

    }

    /**
     * Считывает входной текст посимвольно, буквы сохраняет в мапу.
     * Большие буквы приводит к маленьким
     *
     *
     * @param text - входной текст
     * @return - мапа с частотой вхождения каждой буквы (Ключ - буква в нижнем регистре)
     * Мапа отсортирована по частоте. При итерировании на первой позиции наиболее частая буква
     */
    @NotNull
    Map<Character, Integer> createHist(@NotNull String text) {

    }

```