import com.sun.scenario.effect.impl.sw.sse.SSEBlend_SRC_OUTPeer;

import java.util.*;
import java.time.*;
import java.time.temporal.ChronoUnit;

public class Main {

    private static Scanner input = new Scanner((System.in));

    public static void main(String[] args)
    {
        Catalog catalog = new Catalog();
        LibraryCardManager cardManager = new LibraryCardManager();
        boolean exit = false;

        while (!exit)
        {
            menu();
            System.out.print("Enter the number of the choice you would like to execute: ");
            int choice = Integer.parseInt(input.nextLine());
            System.out.println();
            switch (choice)
            {
                case 1:
                    addToCatalog(catalog);
                    break;
                case 2:
                    addToCardManager(cardManager);
                    break;
                case 3:
                    printAllMaterials(catalog);
                    break;
                case 4:
                    checkOutItem(catalog, cardManager);
                    break;
                case 5:
                    printCopiesCheckedOut(cardManager);
                    break;
                case 6:
                    returnCopy(cardManager);
                    break;
                case 7:
                    returnAllCopies(cardManager);
                    break;
                case 8:
                    renewBook(cardManager);
                    break;
                case 9:
                    exit = true;
                    break;
                default:
                    System.out.print("ERROR: Invalid input!");
            }

            System.out.println();
        }

        System.out.println("PROGRAM TERMINATED");
    }

    public static void menu()
    {
        System.out.println("---------------MENU-------------");
        System.out.println("1 - Add new books/DVDs to the catalog");
        System.out.println("2 - Add new library cards to the card manager");
        System.out.println("3 - See all library materials in the catalog");
        System.out.println("4 - Check out item");
        System.out.println("5 - See all copies checked out to card");
        System.out.println("6 - Return a copy");
        System.out.println("7 - Return all copies");
        System.out.println("8 - Renew a book");
        System.out.println("9 - Exit Program");
    }

    public static void addToCatalog(Catalog catalog)
    {
        String answer;
        do
        {
            System.out.print("Would you like to add a book or dvd? ");
            String item = input.nextLine();

            if (item.equals("book") || item.equals("Book"))
            {
                System.out.print("Enter the title: ");
                String title = input.nextLine();
                System.out.print("Enter the author: ");
                String author = input.nextLine();
                System.out.print("Enter the ISBN #: ");
                String isbn = input.nextLine();
                System.out.print("How many copies of " + "\"" + title + "\"" + " would you like to add to the catalog? ");
                int nCopies = Integer.parseInt(input.nextLine());

                catalog.add( new Book(isbn, title, author), nCopies);
                System.out.println(nCopies + " copies added to the catalog");
            }
            else if (item.equals("dvd") || item.equals("DVD"))
            {
                System.out.print("Enter the title: ");
                String title = input.nextLine();
                System.out.print("Enter the main actor: ");
                String actor = input.nextLine();
                System.out.print("Enter the ISBN #: ");
                String isbn = input.nextLine();
                System.out.print("How many copies of " + "\"" + title + "\"" + " would you like to add to the catalog? ");
                int nCopies = Integer.parseInt(input.nextLine());

                catalog.add( new DVD(isbn, title, actor), nCopies);
                System.out.println(nCopies + " copies added to the catalog");
            }

            System.out.print("\nWould you like to add another book/dvd to the catalog (yes/no)?: ");
            answer = input.nextLine();
        }while( answer.equals("yes") );
    }

    public static void addToCardManager(LibraryCardManager cardManager)
    {
        String answer;
        do
        {
            System.out.print("Enter card ID: ");
            String ID = input.nextLine();
            System.out.print("Enter name: ");
            String name = input.nextLine();

            cardManager.addCard( new LibraryCard(ID, name) );
            System.out.println("Card successfully added to Card Manager\n");

            System.out.print("Would you like to add another card (yes/no)? ");
            answer = input.nextLine();
            System.out.println();
        }while(answer.equals("yes"));
    }

    public static void printAllMaterials(Catalog catalog)
    {
        System.out.println("All Library Materials");
        System.out.println("------------------------");
        for(LibraryMaterial m : catalog.getAllLibraryMaterials() )
        {
            m.print();
            System.out.println();
        }
    }

    public static void checkOutItem(Catalog catalog, LibraryCardManager cardManager)
    {
        System.out.print("Enter library card ID: ");
        String ID = input.nextLine();
        System.out.print("Enter title you want to check out: ");
        String title = input.nextLine();

        LibraryMaterial material = catalog.lookUpTitle(title);
        List<LibraryMaterialCopy> copies = catalog.getAvailableCopies(material);
        if( copies.isEmpty() )
            System.out.println("There are no available copies of " + "\"" + title + "\"");
        else
        {
            LibraryCard card = cardManager.lookUpID(ID);
            card.checkOutItem(copies.get(0));
            System.out.println( "\"" + title + "\"" + " has been successfully checked out");
            System.out.println( "Due Date: " + copies.get(0).getDueDate());
        }
    }

    public static void printCopiesCheckedOut(LibraryCardManager cardManager)
    {
        System.out.print("Enter library card ID: ");
        String ID = input.nextLine();

        LibraryCard card = cardManager.lookUpID(ID);

        System.out.println("All Copies Checked Out");
        System.out.println("-----------------------");
        for(LibraryMaterialCopy copy : card.getCopiesCheckedOut() )
        {
            copy.print();
            System.out.println();
        }
    }

    public static void returnCopy(LibraryCardManager cardManager)
    {
        System.out.print("Enter library card ID: ");
        String ID = input.nextLine();
        System.out.print("Enter title you want to return: ");
        String title = input.nextLine();

        LibraryCard card = cardManager.lookUpID(ID);
        for(LibraryMaterialCopy copy : card.getCopiesCheckedOut() )
            if( copy.title_is(title) )
            {
                card.returnItem(copy);
                break;
            }

        System.out.println("\"" + title + "\"" + " has been returned");
    }

    public static void returnAllCopies(LibraryCardManager cardManager)
    {
        System.out.print("Enter library card ID: ");
        String ID = input.nextLine();
        LibraryCard card = cardManager.lookUpID(ID);
        List<LibraryMaterialCopy> copiesCheckedOut = card.getCopiesCheckedOut();
        for( int i = 0; i < copiesCheckedOut.size(); i++ )
            card.returnItem( copiesCheckedOut.get(i) );

        System.out.println("All copies checked out to card " + ID + " have been returned");
    }

    public static void renewBook(LibraryCardManager cardManager)
    {
        System.out.print("Enter library card ID: ");
        String ID = input.nextLine();
        System.out.print("Enter title of the book you want to renew: ");
        String title = input.nextLine();

        LibraryCard card = cardManager.lookUpID(ID);
        for( LibraryMaterialCopy copy : card.getCopiesCheckedOut() )
        {
            if ( copy.title_is(title) )
            {
                if(copy instanceof DVDCopy)
                    System.out.println("Error: DVD's may not be renewed");
                else
                {
                    card.renewBook( (BookCopy)copy );
                    System.out.println("\"" + title + "\"" + " has been renewed");
                    System.out.println("Due date: " + copy.getDueDate());
                    break;
                }
            }
        }
    }

}
