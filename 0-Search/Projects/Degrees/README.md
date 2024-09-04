# Degrees

Write a program that determines how many "degrees of separation" apart two actors are.

```
$ python degrees.py large
Loading data...
Data loaded.
Name: Emma Watson
Name: Jennifer Lawrence
3 degrees of separation.
1: Emma Watson and Brendan Gleeson starred in Harry Potter and the Order of the Phoenix
2: Brendan Gleeson and Michael Fassbender starred in Trespass Against Us
3: Michael Fassbender and Jennifer Lawrence starred in X-Men: First Class
```

## Background

According to the Six Degrees of Kevin Bacon game, anyone in the Hollywood film industry can be connected to Kevin Bacon with six steps, where each step consists of finding a film that two actors both starred in.

In this problem, we're interested in finding the shortest path between any two actors by choosing a sequence of movies that connects them. For example, the shortest path between Jennifer Lawrence and Tom Hanks is 2: Jennifer Lawrence is connected to Kevin Bacon by both starring in "X-Men: First Class," and Kevin Bacon is connected to Tom Hanks by both starring in "Apollo 13."

We can frame this as a search problem: our states are people. Our actions are movies, which take us from one actor to another (it's true that a movie could take us to multiple different actors, but that's okay for this problem). Our initial state and goal state are defined by the two people we're trying to connect. By using breadth-first search, we can find the shortest path from one actor to another.

## Getting Started

- Download the distribution code from <a href="https://cdn.cs50.net/ai/2023/x/projects/0/degrees.zip" style="color:yellow">THIS LINK</a> and unzip it.

## Understanding 

The distribution code contains two sets of CSV data files: one set in the <code style="color:white">large</code> directory and one set in the <code style="color:white">small</code> directory. Each contains files with the same names, and the same structure, but <code style="color:white">small</code> is a much smaller dataset for ease of testing and experimentation.

Each dataset consists of three CSV files. A CSV file, if unfamiliar, is just a way of organizing data in a test-based format: each row corresponds to one data entry, with commas in the row separating the values for the entry.

Open up <code style="color:white">small/people.csv</code>. You'll see that each person has a unique <code style="color:white">id</code>, corresponding with their <code style="color:white">id</code> in <t style="color:pink">IMDB</t>'s database. They also have a <code style="color:white">name</code>, and a <code style="color:white">birth</code> year.

Next, open up <code style="color:white">small/people.csv</code>. You'll see that each person has a unique <code style="color:white">id</code>, in addition to a <code style="color:white">title</code> and the <code style="color:white">year</code> in which the movie was released.

Now, open up <code style="color:white">small/stars.csv</code>. This file establishes a relationship between the people in <code style="color:white">people.csv</code> and the movies in <code style="color:white">movies.csv</code>. Each row is a pair of a <code style="color:white">person_id</code> value and <code style="color:white">movie_id</code> value. The first row (ignoring the header), for example, states that the person with id 102 starred in the movie with id 104257. Checking that against <code style="color:white">people.csv</code> and <code style="color:white">movies.csv</code>, you'll find that this line is saying that Kevin Bacon starred in the movie "A Few Good Men."

Next, take a look at <code style="color:white">degrees.py</code>. At the top, several data structures are defined to store information from the CSV files. The <code style="color:white">names</code> dictionary is a way to look up a person by their name: it maps names to a set of corresponding ids (because it's possible that multiple actors have the same name). the <code style="color:white">people</code> dictionary maps each person's id to another dictionary with values for the person's <code style="color:white">name</code>, <code style="color:white">birth</code> year, and the set of all the <code style="color:white">movies</code> they have starred in. And the <code style="color:white">movies</code> dictionary maps each movie's id to another dictionary with values for that movie's <code style="color:white">title</code>, release <code style="color:white">year</code>, and the set of all the movie's <code style="color:white">stars</code>. The <code style="color:white">load_data</code> function loads data from the CSV files into these data structures.

The <code style="color:white">main</code> function in this program first loads data into memory (the directory from which the data is loaded can be specified by a command-line argument). Then, the function prompts the user to type in two names. The <code style="color:white">person_id_for_name</code> function retrieves the id for any person (and handles prompting the user to clarify, in the event that multiple people have the same name). The function then calls the <code style="color:white">shortest_path</code> function to compute the shortest path between the two people, and prints out the path.

The <code style="color:white">shortest_path</code> function, however, is left unimplemented. That's where you come in!

## Specification

Complete the implementation of the <code style="color:white">shortest_path</code> function such that it returs the shortest path from the person with id <code style="color:white">source</code> to the person with the id <code style="color:white">target</code>.

- Assuming there is a path from the <code style="color:white">source</code> to the <code style="color:white">target</code>, your function should return a list, where each list item is the next <code style="color:white">(movie_id, person_id)</code> pair in the path from the source to the target. Each pair should be a tuple of two strings.
    - For example, if the return value of <code style="color:white">shortest_path</code> were <code style="color:white">[(1,2), (3,4)]</code>, that would mean that the source starred in movie 1 with person 2, person 2 starred in movie 3 with person 4, and person 4 is the target.
- If there are multiple paths of minimum length from the source to the target, your function can return any of them.
- If there is no possible path between two actors, your function should return <code style="color:white">None</code>.
- You may call the <code style="color:white">neighbors_for_person</code> function, which accepts a person's id as input, and reutrns a set of <code style="color:white">(movie_id, person_id)</code> pairs for all people who starred in a movie with a given person.

You should not modify anything else in the file other than the <code style="color:white">shortest_path</code> function, though you may write additional functions and/or import other Python standard library modules.

## Hints

- While the implementation of search in lecutre checks for a goal when a node is popped off the frontier, you can improve the efficiency of your search by checking for a goal as nodes are added to the frontier: if you detect a goal node, no need to add it to the frontier, you can simply return the solution immediately.

- You're welcome to borrow and adapt any code from the lecture examples. We've already provided you with a file <code style="color:white">util.py</code> that contains the lecture implementations for <code style="color:white">Node</code>, <code style="color:white">StackFrontier</code>, and <code style="color:white">QueueFrontier</code>, which you're welcome to use (and modify if you'd like).

## Testing

If you'd like, you can execute the below (after setting up <a href="https://cs50.readthedocs.io/projects/check50/en/latest/index.html" style="color:pink">check50</a> on your system) to evaluate the correctness of your code. This isn't obligatory; you can simply submit following the steps at the end of this specification, and these same tests will run on our server. Either way, be sure to compile and test it yourself as well!

```
check50 ai50/projects/2024/x/degrees
```

Execute the below to evaluate the style of your code using <code style="color:white">style50</code>.

```
style50 degrees.py
```

<div align=center>
&copy; CS50 AI - Harvard University
</div>