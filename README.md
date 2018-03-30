# all-in-1-blockchain

require  'sinatra'
require 'colorsize'

BALANCES = {
  'allin1' => 1_000_000,
}

PASSWORDS = {
  'allin1' => 'password'
}

#@parum user
get "/balance" do
  user = params ['user']
  puts BALANCES.to_s.yellow
  "#{user} has #{}BALANCES[user]"
end

# param name
post "/user" do
  name = params ['name']
  BALANCES[name] ||= 0
  "OK"
  end

# @param from
# @param to
@ param amount
post "/transfers" do
  from, to = params.values_at('from', 'to').map(&:downcase)
  amount = params['amount'].to_i
  raise unless BALANCES[from] >= amount
  BALANCES[from] -= amount
  BALANCES[to] += amount
  puts BALANCES.to_s.yellow
  "OK"  
end
