# Hard-Problems

1. **15 Days of Learning SQL**

   ```sql
   declare @date date = '3/1/2016'
   declare @days int = 0
   declare @id int
   declare @max int
   declare @people table
   (
   	[hacker_id] int
   )
   declare @results table
   (
   	[date] date,
   	[count] int,
   	[hacker_id] int,
   	[name] nvarchar(max)
   )	
   while(@date < '3/16/2016')
   begin
   	/*
   	2016-03-01 4 20703 Angela
   	2016-03-02 2 79722 Michael
   	*/
   	select
   		@id = null,
   		@max = null
   
   	select @max = max(c) from (
   	select
   		count(*) as c
   	from
   		submissions s
   	where
   		submission_date = @date
   	group by hacker_id
   	) b
   
   	--print @max
   
   
   	select top 1 @id = hacker_id
   	from
   		submissions s
   	where
   		submission_date = @date
   	group by hacker_id
   	having count(*) = @max
   	order by hacker_id
   
   	--print @id
   	insert into @results
   	select
   		@date,
   		count(distinct hacker_id),
   		@id,
   		(Select name from hackers where hacker_id = @id)
   	from
   		submissions s
   	where
   		submission_date = @date
   		and @days = (select count(*) From @people p where s.hacker_id = p.hacker_id)
   
   		
   	insert into @people
   	select
   		hacker_id
   	from submissions s
   	where submission_date = @date and
   		@days = (select count(*) From @people p where s.hacker_id = p.hacker_id)
   	group by
   		hacker_id
   
   
   	select
   		@date = dateadd(d, 1, @date),
   		@days = @days + 1
   end
   
   select * From @results where hacker_id is not null
    order by [date]
   ```

2. **Interviews**

   ```sql
   SELECT ct.contest_id 
   , ct.hacker_id 
   , ct.name
   , sum(isnull(total_submissions,0))
   , sum(isnull(total_accepted_submissions,0))
   , sum(isnull(total_views,0))
   , sum(isnull(total_unique_views,0))
   FROM Contests ct
   inner join Colleges cl
   on ct.contest_id = cl.contest_id
   inner join Challenges ch
   on ch.college_id = cl.college_id
   left join (
       SELECT challenge_id
       , sum(total_views) total_views
       , sum(total_unique_views) total_unique_views
       FROM View_Stats
       GROUP BY challenge_id) v
   on ch.challenge_id = v.challenge_id
   left join (
       SELECT challenge_id
       , sum(total_submissions) total_submissions
       , sum(total_accepted_submissions) total_accepted_submissions
       FROM Submission_Stats
       GROUP BY challenge_id) s
   on ch.challenge_id = s.challenge_id
   group by ct.contest_id 
   , ct.hacker_id 
   , ct.name
   having sum(isnull(total_submissions,0))+sum(isnull(total_accepted_submissions,0))+sum(isnull(total_views,0))+sum(isnull(total_unique_views,0)) > 0
   order by contest_id
   ```
   
   
