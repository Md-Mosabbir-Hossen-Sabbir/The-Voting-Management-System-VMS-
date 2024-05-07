# The-Voting-Management-System-VMS-
 This Voting Management System(VMS)  manages candidate registrations, voter details, and voting center  allocations efficiently. It allows for real-time tracking of votes through a  secure database setup, ensuring transparency and integrity. With built-in  triggers and procedures,
# Fuctionalities of every file of this Project:

# 1.Table.txt :
Use for Create table
# Overview of the Database Schema 
Let’s provide an overview of the database schema for the Voting Management System    
(VMS). The database schema is a crucial component that defines the structure and organization of the data within the system. Here are the key components of the VMS database schema: 
# i. Voter Table: 
o Stores information about registered voters. 
o Includes columns such as voter_ID_no, voter_name, voter_contact_number, and voter_address. 
# ii. Candidate Table: 
o Contains details about candidates participating in the election. 
o Columns include candidate_ID_no, candidate_name, candidate_contact_number, and candidate_address. 
# iii. Symbol Table: 
o Associates symbols (such as party logos or icons) with candidates. 
o Includes columns for symbol_name, symbol_description, and a foreign key referencing the candidate_table. 
# iv. Centre Table: 
o Stores information about voting centers (polling stations). 
o Columns include centre_ID_no, centre_name, and centre_address. 
# v. Vote Information Table: 
o Records each vote cast by a voter. 
o Contains columns for voter_ID_no, symbol_name, centre_ID_no, voting_time, and voting_date. 
# vi. Count Table: 
o Keeps track of the total votes received by each candidate. 
o Includes columns and total_votes. for candidate_name, candidate_symbol,



# 2.Insert.txt:
User for insertion of Data

# 3.Procedure.txt:
We’ve created three stored procedures for your database project. Let’s break down each one:
# p_findname:
o This procedure takes a symbol name (s_name) as input and retrieves the corresponding candidate name (c_name) from the candidate_table.
o It uses a subquery to find the candidate_ID_no associated with the given symbol name in the symbol_table.
o The retrieved candidate name is stored in the c_name output parameter.
# count_total_votes:
o This procedure calculates the total number of votes for a given symbol name (s_name).
o It counts the occurrences of the symbol name in the vote_information table.
o The total votes count is stored in the t_votes output parameter.
# insert_information:
o This procedure inserts information into the count_table.
o It takes the candidate name (c_name), symbol name (s_name), and total votes (t_votes) as input parameters.
o The data is inserted into the count_table

# 4.execute_procedure:
# Initialization:
o we’ve declared variables and types needed for your procedures.
o namearray and countarray are VARRAY types to hold candidate names and vote counts, respectively.
o loop_count, total_symbol, and c_votes are numeric variables.
# Symbol Retrieval:
o You’re retrieving symbol names from the symbol_table and storing them in the s_name_array.
o The loop starts from candidate ID 501 (since you initialized c_votes to 500) and increments it for each symbol.
o Candidate Name Retrieval:
o For each symbol name in s_name_array, you’re using the p_findname procedure to find the corresponding candidate name.
o The candidate names are stored in the c_name_array.
# Vote Count Calculation:
o You’re calculating the total votes for each symbol using the count_total_votes procedure.
o The vote counts are stored in the count_array.
# Inserting Information:
o Finally, you’re inserting the candidate name, symbol name, and vote count into the count_table

# 5.Trigger.txt:
# Trigger Purpose:
o The trigger is defined to execute before an update operation on the symbol_name column of the symbol_table.
# Variables:
o before_symbol: Holds the old value of the symbol_name before the update.
o after_symbol: Holds the new value of the symbol_name after the update.
o v_id: Used to store the voter ID during cursor iteration.
o flag: Indicates whether the candidate symbol exists in the count_table.
# Cursor and Loop:
o A cursor named ct retrieves the voter IDs associated with the old symbol name (before_symbol) from the vote_information table.
o The loop iterates through each voter ID and updates their vote to the new symbol name (after_symbol).
# Update Count Table:
o If the flag is greater than 0 (meaning the candidate symbol exists in the count_table), the trigger updates the candidate symbol to the new value.

# 6.Execute_trigger.txt:
o Show intial Data and update data

# 7.Calculate_winner.txt:
# Initialization:
You’ve declared several variables:
o c_name: Candidate name.
o s_name: Symbol name (same as candidate name).
o t_votes: Total votes for a candidate.
o max_votes: Maximum total votes across all candidates.
o winner_number: Number of candidates with the maximum votes.
# Finding Maximum Votes:
o The first query retrieves the maximum total votes from the count_table.
o The second query counts how many candidates have the maximum votes.
# Handling Tie:
o If there is more than one candidate with the same maximum votes, you print a message indicating a tie.
# Cursor and Loop:
o If there’s only one winner, a cursor named ct retrieves candidate information (name, symbol, and total votes) for the winner(s).
o The loop prints each winner’s details.

# 8.Delete_trigger.txt:
# Trigger Purpose:
o The trigger is defined to execute before a delete operation on the candidate_table.
Variables:
o c_id: Holds the candidate ID being deleted.
o s_name: Holds the symbol name associated with the candidate.
o flag: Indicates whether the candidate symbol exists in the count_table.
# Symbol and Vote Deletion:
o The trigger retrieves the symbol name associated with the candidate being deleted.
o It deletes corresponding records from the vote_information and symbol_table.
# Update Count Table:
o If the flag is greater than 0 (meaning the candidate symbol exists in the count_table), the trigger also deletes the candidate’s entry from the count_table

