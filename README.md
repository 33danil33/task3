import java.util.*;

public class PhoneBook {
    public static void main(String[] args) {
        HashMap<String, List<String>> phoneBook = new HashMap<>();

        addPhoneNumber(phoneBook, "Иванов", "123456789");
        addPhoneNumber(phoneBook, "Петров", "987654321");
        addPhoneNumber(phoneBook, "Сидоров", "111111111");
        addPhoneNumber(phoneBook, "Иванов", "222222222");
        addPhoneNumber(phoneBook, "Сидоров", "333333333");
        addPhoneNumber(phoneBook, "Иванов", "444444444");

        List<Map.Entry<String, List<String>>> sortedEntries = sortByPhoneNumberCount(phoneBook);

        for (Map.Entry<String, List<String>> entry : sortedEntries) {
            String name = entry.getKey();
            List<String> phoneNumbers = entry.getValue();
            System.out.println(name + ": " + phoneNumbers.size() + " телефон(ов)");
            for (String phoneNumber : phoneNumbers) {
                System.out.println("- " + phoneNumber);
            }
        }
    }

    private static void addPhoneNumber(HashMap<String, List<String>> phoneBook, String name, String phoneNumber) {
        if (phoneBook.containsKey(name)) {
            List<String> phoneNumbers = phoneBook.get(name);
            phoneNumbers.add(phoneNumber);
        } else {
            List<String> phoneNumbers = new ArrayList<>();
            phoneNumbers.add(phoneNumber);
            phoneBook.put(name, phoneNumbers);
        }
    }

    private static List<Map.Entry<String, List<String>>> sortByPhoneNumberCount(HashMap<String, List<String>> phoneBook) {
        List<Map.Entry<String, List<String>>> sortedEntries = new ArrayList<>(phoneBook.entrySet());

        sortedEntries.sort((entry1, entry2) -> entry2.getValue().size() - entry1.getValue().size());

        return sortedEntries;
    }
}
