CREATE DATABASE IPL;

create table matches(
id integer,

season integer,

city varchar(222),

date date,

team1 varchar(222),

team2 varchar(222),

toss_winner varchar(222), 

toss_decision varchar(222),

result varchar(222),

dl_applied integer,

winner varchar(222),

winner_by_runs integer,

winner_by_wicket integer,

player_of_the_watch varchar(222),

venue varchar(222),

empire1 varchar(222),

empire2 varchar(222)
);


create table deliveries(

matchid integer,

innings integer,

bating_team varchar(222),

bowling_team varchar(222),


 which_over integer,
 
ball integer,


batsman varchar(222),

non_striker varchar(222),

bowler varchar(222),

is_super_over integer,

wide_runs integer,

bye_runs integer,

legbye_runs integer,

noballs_runs integer,

penalty_runs integer,

batsman_runs integer,

extra_runs integer,

total_runs integer,

player_dismissed varchar (222),

dismissal_kind varchar(222),

fielder varchar(222)

);

SELECT * FROM ipl.deliveries;

select * FROM ipl.matches;

select * from ipl.matches limit 5;

# 1.How many players have won player of the match award at least once??
select count(player_of_match) FROM  ipl.matches;

# 2.Find season winner for each season (season winner is the winner of the last match of each season
select distinct(season),winner,date,id from ipl.matches
order by season,date desc;
# 3.Get details of top 5 matches which were won by maximum number of runs??
select * from ipl.matches
order by win_by_runs desc
limit 5;


# 4.Order the rows by city in which the match was played??
select * from ipl.matches 
order by city  limit 10;

# 5.Find venue of 10 most recently played matches??
select  venue from ipl.matches
order by date desc
limit 5;


# 6.Return a column with comment based on total_runs
select batsman,total_runs ,
case 
when total_runs=4 then 'four'
when total_runs=6 then 'six'
when total_runs=0 then 'bolt'
when total_runs=1 then 'single'
end  as howzthat 
from 
ipl.deliveries;
select max(win_by_runs)  from ipl.matches;
  ##how many extra runs have been conceded in ipl???
  select sum(extra_runs) from ipl.deliveries;
  
  
  ##On an average, teams won by how many runs in ipl??
  select ceil(avg(win_by_runs)) from matches;
  
  ##How many extra runs were conceded in ipl by SK Warne???
  select sum(extra_runs ) from deliveries
  where bowler='SK Warne';
  
  
 # 7.How many boundaries (4s or 6s) have been hit in ipl???
  select count(total_runs) from deliveries
  where total_runs=4 or total_runs=6;
  
  
  # 8.How many balls did SK Warne bowl to batsman SR Tendulkar
  select  count(ball)from ipl.deliveries
  where bowler='SK Warne' and batsman='SR Tendulkar';
  # 9.how many matches were played in month of april??
  SELECT COUNT(*) FROM matches WHERE EXTRACT(month FROM date) = 4;
  
  # 10. How many matches were played in the March and June??
  select count(* ) from matches where extract(month from date)=3 or EXTRACT(month FROM date) = 6;
  ##Total number of wickets taken in ipl (count not null values)??
  select count(player_dismissed) as wickets from  deliveries
  where player_dismissed is not null;
  
  # 11. How many batsmen have names starting with S?
  select count(distinct(batsman)) from deliveries
  where batsman like 'S%';
  ##how many teams have the word royal in it???
  select * from matches
  where team1 like '%royal%' or team2 like '%royal%';
  
  # 12. Maximum runs by which any team won a match per season???
select season, max(win_by_runs) from matches
  group by season
  order by season;
  
  
