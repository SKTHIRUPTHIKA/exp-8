package multithreadingdemo;

import java.util.Scanner;

class WordThread implements Runnable {
    String text;

    WordThread(String text) {
        this.text = text;
    }

    public void run() {
        String[] words = text.split("\\s+");
        System.out.println("\n--- Words ---");
        for (String w : words) {
            System.out.println(w);
            try {
                Thread.sleep(2000); // 2-second delay between each word
            } catch (InterruptedException e) {
                System.out.println("WordThread interrupted");
            }
        }
    }
}

class VowelThread implements Runnable {
    String text;

    VowelThread(String text) {
        this.text = text;
    }

    public void run() {
        System.out.println("\n--- Vowels ---");
        for (char c : text.toCharArray()) {
            if ("AEIOUaeiou".indexOf(c) != -1) {
                System.out.println(c);
                try {
                    Thread.sleep(2000); // 2-second delay between each vowel
                } catch (InterruptedException e) {
                    System.out.println("VowelThread interrupted");
                }
            }
        }
    }
}

public class RunnableExample {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("URK24CS1269 - S K THIRUPTHIKA");
        System.out.println("Exercise 8: Multithreading using Runnable Interface\n");

        System.out.print("Enter a paragraph: ");
        String text = sc.nextLine();

        // Create thread objects
        Thread t1 = new Thread(new WordThread(text));
        Thread t2 = new Thread(new VowelThread(text));

        // Start first thread (words)
        t1.start();
        try {
            t1.join(); // Wait until the word thread finishes
        } catch (InterruptedException e) {
            System.out.println("Main thread interrupted during WordThread execution");
        }

        // Start second thread (vowels)
        t2.start();
        try {
            t2.join(); // Wait until the vowel thread finishes
        } catch (InterruptedException e) {
            System.out.println("Main thread interrupted during VowelThread execution");
        }

        System.out.println("\nExecution completed successfully!");
        sc.close();
    }
}
