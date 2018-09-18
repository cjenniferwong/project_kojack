# Project Summary:
I analyzed the Soundcloud network in the hopes to leverage the data that I've gathered to implement a social network-supplemented recommendation system to see if that makes better recommendations as opposed to using similar users across the entire network for new users [with limited data].

## Problem Statement:
I am interested in exploring social relationships and recommender systems. Upon further research, I found that there are several papers published in academia which explored the idea of using social networks as a way to solve the cold-start problem in collaborative filtering for new users. Traditionally, collaborative filtering techniques fall short for new users, because there isn't enough data to find similar users, and from there get recommendations. By leveraging the user's social network, others have been able to provide significantly better recommendations.

The platform allows users to follow other users for their streams to show up on their timeline. The idea for this project was that 'birds of a feature, flock together', and I wanted to see if leveraging your friends would improve the songs that I would recommend as opposed to comparing it similar users across the network.

The scope of this project was to try to see if this was applicable for the Soundcloud network. I would first have to do some analysis on the network, and then taking the data that I've gather I would try to implement the social nework recommendation system. 

## Data
Getting the data was a toughy. Soundcloud actually closed the application to get client id's for third party users to access their API. poop. But after figure out a way around that, I was left with a treasure trove of data and (pretty much) unlimited calls. Amazing.

SOo I looked that the top songs chart that Soundcloud implemented in order to find a way of identifying general genres on the platform objectively. From there, I was able to gather the top 11 genre (determined by the number of plays from the top songs being beyond my threshold of over 45,000 plays ever). I took artists from these genres, and found a random follower in order to 'seed' the network I was trying to build. The reason behind this was because if I were to seed with the actual popular artist in the network, then getting their followers and following would prove to be a huge undertaking.

From the seeds, I gathered their follower and following data as well as the songs that they liked and [essentially] reposted on their profiles. To grow the network, I took a minimum between 5 and the number of followers that they actually had, and continued to build a sample network of Soundcloud through breadth-first search approach. 

All the data was gathered on *AWS instances* and stored in a *Mongo Database*.

## Dater Science 
From the data that I gathered, I was able to get almost 250k unique users and almost a million edges/relationships in my directed network. I queried my data from the mongo db and put them into Gephi in order to get additional information to gather insight into the structure of the network.

From gephi, I was able to determine *authorities* in the network based on the calculated eigencentrality score of each user, as well as *communities* in the BFS network from the modularity function. After exploring the communities, I found that they were sub-genres of the network! I thought that was really interesting. Unsurprisingly, there are a lot of communities which appreciate different nuances of rap and hip-hop. This is because soundcloud is known to be a platform for which aspiring hip-hop artists and rappers can distribute their art and grow a dedicated fanbase. This is especially in recent years in which the new generation of successful rappers which humble beginnings on soundcloud started to gain mainstream traction.

I also additional insight into soundcloud platform and [possible] current health. Intuitively, I would have guessed that the more followers a user has is correlated with their eigencentrality score. This is under the assumption that the followers were gained organically in which work published gained traction and elicited genuine interest in the artist.

After looking at the distribution of eigencentrality, I was surprised to find my intuition was false. In fact, the user with the most number of followers in my network had one of the lowest eigencentrality score. Upon unearthing this factoid, I devled deeper in my analysis and tried to find additional information that would help me better understand what was going in.

In *tableau* I binned the followers into buckets, and visualized the average eigencentrality score of each bucket. This showed me a normal distribution when I didn't expect to find one. Else, it shows me that most genuine users who gained a following organically had between 1-5k followers.

In conclusion, I think that soundcloud has a problem with bots which artificially inflate someone's number of followers. Soundcloud also has a problem with lots of users with less than 100 followers. What this suggests to me is that not enough people are suggesting that their friends get on Soundcloud.

So how do we fix this problem?

## Future Directions
I couldnt get my SVD recommender to work nor predict links between users/songs. I would like to do that over the next couple of days while professor kiwi is forced to hang out at Metis from the hours of 9-5PM.

Thank you for listening to my TED talk. Please follow me on soundcloud.
_________________
August 27th. 2018

I wonder if you can have multiple instances on aws scraping (to utilize the different IP addresses) so that I can maximize the rate of data I can get for my project. I'd rather have most of my data at the start of my project. OH! Vivien did something similar to this for her last project so I should see if she can help me with that.


September 6th, 2018
Dear Diary, 
It's been a while since I've written in you. I just released my scraper into the world seeded it with Sarah Jake's follower (notatyourparty).
Next Steps would be to release a similar notebook but with a different seed. Someone who is in a different music genre.

Here is the running list of seeds.
1. 477797010



Afterwards, I need to get the tracks and likes from each person in my database. Omg.

Note to self:
I should probably get a list of all the users who I've gotten the likes and streams of and put that in a set.
The put the followers and following users in a set
take the difference
and use that as my queue!
