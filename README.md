  import java.util.Random;

    public class Deck
    {
private Card[] myCards;
private int numCards;

    // This constructor builds a deck of 52 cards.
public Deck()
{
    int c = 0;
    this.numCards = 52;
    this.myCards = new Card[this.numCards];

    for(int i = 0; i < 4; i++){
        for(int j = 1; j <= 13; j++){
            this.myCards[c] = new Card (i, j);
            c++;
        }
    }
  }

public Card deal()
{
    Card top = this.myCards[0];

        for (int c=1; c<this.numCards; c++){
            this.myCards[c-1]=this.myCards[c];
        }
        this.myCards[this.numCards-1]=null;
        this.numCards--;
        return top;
}

public boolean isEmpty()
{
    if (numCards == 0 ){
        return true;
    } else {
        return false;
    }
}

public void shuffle(){

    Random rng = new Random();

    Card temp;

    int j;
    for(int i = 0; i < this.numCards; i++){
        j = rng.nextInt(this.numCards);
        temp = this.myCards[i]; 
        this.myCards[i]= this.myCards[j];
        this.myCards[j] = temp;
    }
}

public void printDeck(int numToPrint){
    for (int c = 0; c<numToPrint; c++){
            System.out.printf("% 3d/%d %s \n",      c+1 ,this.numCards, this.myCards[c].toString());
        }

        System.out.printf("\t\t[%d other]", this.numCards- numToPrint);
}
    }
    
 // This class represents one playing card.
     public class Card{

// Card suits (provided for your convenience - use is optional)
public static final int SPADES   = 0;
public static final int HEARTS   = 1;
public static final int CLUBS    = 2;
public static final int DIAMONDS = 3;

// Card faces (provided for your convenience - use is optional)
public static final int ACE      = 1;
public static final int TWO      = 2;
public static final int THREE    = 3;
public static final int FOUR     = 4;
public static final int FIVE     = 5;
public static final int SIX      = 6;
public static final int SEVEN    = 7;
public static final int EIGHT    = 8;
public static final int NINE     = 9;
public static final int TEN      = 10;
public static final int JACK     = 11;
public static final int QUEEN    = 12;
public static final int KING     = 13;


// define fields here
private int suit;
private int face;
private Suit mySuit;
private int cardValue;

public Card(int cardSuit, int cardFace)
{
    this.suit = cardSuit;
    this.face = cardFace;
}

// This method retrieves the suit (spades, hearts, etc.) of this card.
public int  getSuit()
{
    return suit;
}

// This method retrieves the face (ace through king) of this card.
public int getFace()
{
    return face;
}

    public int getValue()
{
    if (face>=2 && face<=10){
        return face;
    } else if (face>= 11 && face<=13){
        return 10;

    } else {
        return 1;
    }
}

public String toString(){

    String str = "Error";

    switch(this.face){

    case 1:
        str = " Ace";
        break;

    case 2:
        str = "Two";
        break;

    case 3:
        str = "Three";
        break;

    case 4:
        str = " Four";
        break;

    case 5:
        str = "Five";
        break;

    case 6:
        str = "Six";
        break;

    case 7:
        str = " Seven";
        break;

    case 8:
        str = "Eight";
        break;

    case 9:
        str = "Nine";
        break;

    case 10:
        str = " Ten";
        break;

    case 11:
        str = "Jack";
        break;

    case 12:
        str = "Queen";
        break;

    case 13:
        str = " King";
        break;

                }
    return str + " of " + this.suitToString(suit);
}

public String suitToString(int a ){

    String b;
    if(a == 0){
        b = "Spades";
        return b;
    }else if (a == 1){
        b = "Hearts";
        return b;
    }else if (a == 2){
        b = "Clubs";
        return b;
    }else {
        b = "Diamonds";
        return b;
    }
}
}
 public class Player {

public String name;
private double bankRoll;
private Card[] hand;
private double currentBet;
private int numCards = 0;

public double getCurrentBet() {
    return currentBet;
}

public void setCurrentBet(double currentBet) {
    this.currentBet = currentBet;
}

public double getBankRoll() {
    return bankRoll;
}

public Card[] getHand() {
    return hand;
}

public Player(String name, double amount){
    this.name = name;
    this.bankRoll = amount;
    this.currentBet = 0;
    this.hand = new Card[11];
}

public void resetHand(){
    this.hand = new Card[11];
    this.numCards = 0;
}

public String toString(){
    return this.name + " - $" + this.bankRoll + printHand();
}

public void addCard2(Card c){
    this.hand[this.numCards] = c;
    numCards ++;
}

public String printHand(){
    String handString = "";
    for (int i = 0; i<this.numCards; i++){
        handString += this.hand[i] + ";" ;
    }
    return handString;
}
public boolean addCard(Card aCard){

    if(this.numCards ==10){
        System.err.printf("%s's hand already has 10 cards\n", 

    this.name );
        System.exit(1);
    }
    this.hand[this.numCards]=aCard;
    this.numCards++;
    return(this.getHandSum()<=21);
}
public int getHandSum(){
    int handSum = 0;
    int cardNum;
    int numAces = 0;

    for (int c=0; c<this.numCards; c++){
        cardNum = this.hand[c].getValue();

        if(cardNum == 1){
            numAces++;
            handSum+=11;
            } else if (cardNum > 10){
                handSum+=10;
            }else {
                handSum += cardNum;
            }

    }

    while (handSum >21 && numAces > 0){
        handSum -= 10;
        numAces --;
    }

    return handSum;
}

public void showHand(boolean showFirstCard){
    System.out.printf("%s's cards:", this.name);
    System.out.println();
    for(int c = 0; c<this.numCards; c++){
        if(c==0 && !showFirstCard){
            System.out.println(" [hidden]");
            } else {
                System.out.printf(" %s", this.hand[c].toString());
                System.out.println();
            }
    }

}
private int face;

public int getFace()
{
    this.face = face;
    return face;
}

 public class Blackjack {

public static void main(String[] args) {

    Deck myDeck = new Deck();
    myDeck.shuffle();

    System.out.print("Enter number of Players (Max 6): ");
    int numPlayers = IO.readInt();
    double[] playersBank = new double[numPlayers];
    if (numPlayers<0 || numPlayers>6){
        IO.reportBadInput();
    }
    Player[] player = new Player[numPlayers];
    Player dealer = new Player ("Dealer", 0);

    for (int i =0; i<numPlayers; i++){
        System.out.print("Enter player's name: ");
        String playerName = IO.readString();

        System.out.println();

        System.out.print("Enter player's starting balance:");
        double startingBalance = IO.readDouble();
        System.out.println();
        playersBank[i]= startingBalance;
    Player a;

            a = new Player(playerName, startingBalance);
        player[i] = a;

        System.out.print(player[i]+ " ");
        System.out.println();

        }
    double currentBet;
    double[] bets = new double[player.length];

    for (int i=0;i<player.length; i++){

        System.out.println(player[i]+" "+"enter current bet:");
        currentBet = IO.readDouble();
        if(currentBet> player[i].getBankRoll()){
            System.out.println("That is greater than the amount in your account");
            return;
        }
        bets[i]= currentBet;

    }

    for(int i = 0;i<player.length; i++){

            player[i].addCard(myDeck.deal());
            player[i].addCard(myDeck.deal());
            player[i].showHand(true);
            System.out.println(player[i].getHandSum());
        }

    for(int i=0; i<1;i++){
        dealer.addCard(myDeck.deal());
        dealer.addCard(myDeck.deal());
        dealer.showHand(false);
    }

    for(int i=0; i<player.length; i++){
        dealer.showHand(false);

        if(dealer.getHandSum() - 10 == 11){
            player[i].showHand(true);
            System.out.println("Would you like insurance? (y) or (n)");
            String ans = IO.readString();
            ans.toLowerCase();
            if(ans.equalsIgnoreCase("y")){
                System.out.println("How much would you like to bet?");
                int answer = IO.readInt();
                if(dealer.getHandSum() == 21){
                    playersBank[i] -= bets[i];
                }
                }

        }

        }

    for(int i=0; i<player.length;i++){

        int numCards = 2;
        boolean playerDone = false;
        boolean dealerDone = true;
        String ans = "";
        boolean doubleDown;

        if(player[i].getBankRoll() - bets[i] > 0){
        System.out.println(player[i].name+" Your hand value is: "+ player[i].getHandSum());
        System.out.println("Would you like to double down? (Y or N)");
        ans = IO.readString();
        ans.toLowerCase();

        if(ans.equalsIgnoreCase("y") ){
            player[i].addCard(myDeck.deal());
            bets[i]= bets[i]*2;
            doubleDown = true;
            player[i].showHand(true);
            playerDone = true;

            }}else {break;}

        System.out.println(player[i].name+" Your hand value is: "+ player[i].getHandSum());
        System.out.println();
        System.out.println("Enter 1 to hit 2 to stay");
        System.out.println(player[i].getHandSum());
        int answer = IO.readInt();
        while(answer == 1 && player[i].getHandSum()<21){
             player[i].addCard(myDeck.deal());
             player[i].showHand(true);
             if(player[i].getHandSum() > 21){
                 System.out.println("You busted");
                 playerDone = true;
                 break;
             }
             System.out.println();
             System.out.println(player[i].name + "Your hand value is: " + player[i].getHandSum());
             System.out.println();
                System.out.println("Enter 1 to hit 2 to stay");
                answer = IO.readInt();

        if(player[i].getHandSum() > 21){
             System.out.println("You busted");
             playerDone = true;
         }else if (answer == 2){
            playerDone = true;
            dealerDone = true;
            continue;

        }

        }

        boolean allPlayersDone = true;
        dealerDone = false;

    if(allPlayersDone && !dealerDone){

        dealer.showHand(true);
        System.out.println();

        if(dealer.getHandSum()==21 && dealer.getHand().length == 2){
            System.out.println("Dealer has blackjack");
            dealerDone=true;
        }else while(dealer.getHandSum()<17){
            dealer.addCard(myDeck.deal());
            dealerDone = false;
        }}else if(dealer.getHandSum()>=17 && dealer.getHandSum()<22){
            System.out.println("Dealer Stays.");
            System.out.print(dealer + "Hand value is:" + dealer.getHandSum());
            dealerDone = true;
        }
    }

boolean winCheck = true;

if(winCheck == true){
for (int i=0; i<player.length;i++){
int playerValue = player[i].getHandSum();
int dealerValue = dealer.getHandSum();

    player[i].showHand(true);
    dealer.showHand(true);
    System.out.println();
    if(playerValue > 21){
        System.out.println(player[i].name + " You Busted You Lose " + bets[i] + " will be deducted from your account." + " $"+ playersBank[i] + " is left in your account");
        double temp = playersBank[i] - bets[i];
        playersBank[i] = temp;
    }
    if(dealerValue > playerValue){
        System.out.println( player[i].name + " You lose "+ bets[i]+ " Will be deducted from your account" + " $"+ playersBank[i] + " is left in your account");
        double temp = playersBank[i]-bets[i];
        playersBank[i] = temp;
    }else if(dealerValue > 21 && playerValue <= 21 ){
        System.out.println(player[i].name + " You win "+ bets[i]+ " Will be added to your account" + " $"+ playersBank[i] + " is left in your account");
        double temp = playersBank[i]+bets[i];
        playersBank[i] = temp;
    }else if(playerValue==dealerValue){
        System.out.println(player[i] + " Push:  Bet is unchanged"+ " $"+playersBank[i] + " is left in your account");

    }
}
}
}

    }
