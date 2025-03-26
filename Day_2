import Nat "mo:base/Nat";
import Float "mo:base/Float";
import Array "mo:base/Array";
import Time "mo:base/Time";

actor Transaction {

  stable var balance : Float = 100;
  stable var transactions : [Transaction] = [];
  stable var transactionId : Nat = 0;

  type Transaction = {
    id : Nat;
    message : Text;
    timeStamp : Time.Time
  };
  func recordTransac(message : Text) {
    var transaction : Transaction = {
      id = transactionId;
      message = message;
      timeStamp = Time.now()
    };
    transactions := Array.append(transactions, [transaction]);
    transactionId += 1;

  };

  public func checkBalance() : async Text {
    var message = "Your balance is " # Float.toText(balance);
    recordTransac(message);
    return message
  };

  public func topUp(amount : Float) : async Text {
    balance := balance + amount;
    var message = "You deposited: " # Float.toText(amount);
    recordTransac(message);
    return message
  };

  public func withdrawalBalance(amount : Float) : async Text {
    if (amount > balance) {
      return "Insufficient fund"
    }

    else {
      balance := balance - amount;
      var message = "You withdrew: " #Float.toText(amount);
      recordTransac(message);
      return message
    }
  };

  public func getTransactions() : async [Transaction] {
    return transactions
  }

}
