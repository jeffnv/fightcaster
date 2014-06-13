fightcaster
===========

### MVP
0. User Accounts
0. Facebook Login
0. Submit picks for upcoming fight
0. Publish results after fight is over
0. Calculate score based on picks <=> results  

competetive fight picking

* can see all the picks you and friends have
* cannot pick fights that have already happened, or have started
* compare results to get a score for predictions
* rank users on picks

user
  Name
  * has_many friends through friendship

friendship
  friender_id
  friendee_id

event
  date
  location
  * has many matchups

matchup
  event_id
  rounds
  fighter1_id
  fighter2_id
  result_id - the actual result of the fight, initially null
  * belongs to event
  * belongs to actual_result of fight
  * has_many predictions (results) (don't include the one we belong to)

fighter
  name
  * has_many matchups

result
  matchup_id
  winning_figher_id (null if no contest/draw)
  * belongs_to matchup
  * has_one finish (or none)
  * has_one prediction
  * has_one predictor through prediction

finish
  result_id
  finish_round - [1-5]
  finish_time - (null if decision)
  finish_method - ('sub', 'ko')
  * belongs_to result

prediction
  user_id - person who submitted the prediction
  result_id - the prediction
  * belongs_to predictor
  * belongs_to result
