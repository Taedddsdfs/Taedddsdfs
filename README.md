import java.util.Scanner;
import java.util.ArrayList;


	/*
	 Creator: TaeHunKim G12;
	 
	 BlackJack: Player vs Dealer battle
       The person who gets sum of 21 or close to 21 wins the game. 
       Ace = 1 or 11.
       Jack, King, Queen= 10 
       numbered cards = exact numbers
       After placing a bet, all players and dealers are dealt two cards.
       The dealer opens one of his cards.
       The dealer must draw additional cards until the sum of cards is 17.
        A player may receive (Hit) or not receive (Stay) additional cards as long as the sum of the cards does not exceed 21.
	 */

public class Main {
	
static int cardNow;
static ArrayList <Card> deck = new ArrayList <Card> ();
static Scanner sc = new Scanner(System.in);	
   public static int []cardSort = {0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51};

	public static void main(String[] args){
		for(int k=0;k<100;k++){
	      //Create a deck of cards having
		
	      String [] cardName = {"Spade Ace","Spade 2", "Spade 3","Spade 4","Spade 5","Spade 6","Spade 7","Spade 8","Spade 9","Spade 10","Spade Jack","Spade Queen","Spade King",
	    		  "Diamond Ace","Diamond 2", "Diamond 3","Diamond 4","Diamond 5","Diamond 6","Diamond 7","Diamond 8","Diamond 9","Diamond 10","Diamond Jack","Diamond Queen","Diamond King",
	    		  "Heart Ace","Heart 2", "Heart 3","Heart 4","Heart 5","Heart 6","Heart 7","Heart 8","Heart 9","Heart 10","Heart Jack","Heart Queen","Heart King",
	    		  "Club Ace","Club 2", "Club 3","Club 4","Club 5","Club 6","Club 7","Club 8","Club 9","Club 10","Club Jack","Club Queen","Club King"
	      };
	     
			
		
	
	      System.out.println("Display New Deck!");

	     
	
	for(int i=0;i<52;i++) {
		 Card cbuf = new Card(cardName[i]);
		deck.add(cbuf);
	}
	
	      
	      displayDeck(deck);
	      
	      
	      
	      System.out.println("\nDisplay Shuffled Deck");
	      Shuffle();
	      displayDeck(deck); 
	      
	      //Start Game
	      
		  System.out.print("Dealer's cards: "+ " ");
		     
		  System.out.print(Hit(1)+" ");
		  System.out.print("and Hidden card drawn.");

	 	  Hit(1);
	    		 	  
	 	  
	 	 System.out.printf("\n");
	 	 System.out.print("Player's cards:" +" ");
	 	 
		  System.out.print(Hit(2) + " ");
		  System.out.print(Hit(2)+ " ");
	 	
	     for(int i=0;i<100;i++) {
	    	 
		    System.out.print("Player's point:"+" ");
		    System.out.print(sumofValue(2));
		    if(sumofValue(2)>21) {
		    	System.out.println("Player's point:"+ sumofValue(2));
		    	System.out.println(" "+"Bust! Player lost and Dealer won!");
		    	
			      System.exit(0);

		    }
		    else if(sumofValue(2)==21) {
		    System.out.println("BlackJack!Player won!");
		   
		      System.exit(0);

		    }
		    System.out.println(" "+"You want to hit or stand ? Press H for hit and S for stand.");
		    
		    if(sc.next().equals("H")) {
		    Hit(2);	
		    }
		    else {
		    Stand();
		    break;
		    }
	     }
	     
	     // variable sum
		  
		
	 
	      while(sumofValue(1)<17) {
	    	  Hit(1);
	      }
	      
	      if(sumofValue(1)>21) {
	    	System.out.println("Dealer's point:"+ sumofValue(1));
		    System.out.println("Bust! Dealer lost! Player won!");
		    System.exit(0);

	      }
		   else if(sumofValue(1)==21) {
		    System.out.println(" "+"BlackJack! Dealer won!");
		      System.exit(0);

		    }
	      
		    else if(sumofValue(2)>=sumofValue(1) && sumofValue(2)<21) {
		    	while(sumofValue(2)>sumofValue(1)) {
		           Hit(1);
		    	}
		    	if(sumofValue(1)>21) {
		    		 System.out.println("Player's point:"+ sumofValue(2));
			 		    System.out.println("Dealer's point:"+ sumofValue(1));
			    		 System.out.println("Bust! Dealer lost! Player won!");
			   	      System.exit(0);
		    	}
		    	else if(sumofValue(2)==sumofValue(1)) {
		    		 System.out.println("Player's point:"+ sumofValue(2));
		 		    System.out.println("Dealer's point:"+ sumofValue(1));
		    		 System.out.println("Push! Tied!");
		   	      System.exit(0);

		    	}
		    	else if(sumofValue(1)>sumofValue(2)) {
		    		 System.out.println("Player's point:"+sumofValue(2));
		 		    System.out.println("Dealer's point:"+ sumofValue(1));
		    		 System.out.println("Dealer won!");
		   	      System.exit(0);

		    	}
		    	
		    	else if(sumofValue(1)<sumofValue(2)) {
		    		 System.out.println("Player's point:"+sumofValue(2));
		 		    System.out.println("Dealer's point:"+ sumofValue(1));
		    		System.out.println("Player won!");
		  	      System.exit(0);

		    	}
		    	
		    
		    }
		   }
	}

	
	



		
	
	     

//functions I made:)

//Literally displaying deck
	public static void displayDeck(ArrayList<Card> deck) {
	    for (int i =0; i<deck.size(); i++){
	       System.out.println(deck.get((int)cardSort[i]).getCardName());
	 }
	}
	
	
	
	
		
	//Hit(1) for dealer Hit(2) for player drawing card
	public static String Hit(int phit) {
		String a = null;
		 
		a = deck.get((int)cardSort[cardNow]).getCardName();
	    deck.get((int)cardSort[cardNow]).setWho(phit);	    
	    cardNow++;
	    
		 return a;
	}
	
	
	
	
	public static String Stand() {
		return "Player stated 'Stand'. Dealer's turn.";
		
	}

	
	
	//Getting the total points!
	
	
	public static int cardValue(int p) {				
		for(int i = 0; i <= 12; i++) {
			if(p % 13 == i) {
				if(i >= 9 && i <= 12){//j == 11 q == 12 k == 13
					return 10;
				}
				else {
					return i + 1;			
				}
	
			}
				
		}		
		return 0;
		
	}
	
	public static int sumofValue(int p) {
		int sum = 0;
		int aCount = 0;
		for(int i=0; i<52;i++) {
			if(deck.get(i).getWho() == p) {
				
				if(i % 13 == 0) {
					sum++;
					aCount++;
				}
				else {
					sum += cardValue(i);								 													 
				}
			}				
		}
		if(aCount > 0) {
			for(int i = 1; i <= aCount; i++) {
				if(sum + i * 10 > 21)
					break;
				sum += (i * 10);
			}
		}
		else
		return sum;
		{
			return sum;
		}
	
	}
	
	
// Basically Shuffling.
	public static void Shuffle() {
    for(int i = 0; i < 52; i++) {
  	 
  	 int temp1 = (int)(Math.random()*52);
	    int temp2 = (int)(Math.random()*52);
	    int temp3 = cardSort[temp1];
	    cardSort[temp1] = cardSort[temp2];
	    cardSort[temp2] = temp3;
    }
}
}

