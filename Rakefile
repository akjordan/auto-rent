task :auto_rent do
	require 'net/http'
	require 'date'
	require 'twilio-ruby'

	venmotoken = 'Avxxxxxxxxxxxxxxxxxxx'

	# twilio credentials
	account_sid = 'ACxxxxxxxxxxxxxxxxxxx'
	auth_token = 'e3xxxxxxxxxxxxxxxxxxx'
		
	date = DateTime.now.to_date
	day_to_bill = 25

	begin
		if date.day == day_to_bill

			# name of each renter and then their venmo user_id and the amount you want to charge them
			renters = { "Arielle" => ["1111111111111111111","-500"], "Leslie" => ["1111111111111111111","-750"],
			"Evan" => ["1111111111111111111","-1000"], "Dana"  => ["1111111111111111111", "-1250"] }

			renters.each do |name, value|
				user = value[0]
				amount = value[1]
				note = "Hello #{name}! Please pay your rent of $#{amount} for #{date.next_month.mon}/#{date.next_month.year}."
				uri = URI('https://api.venmo.com/v1/payments')
				res = Net::HTTP.post_form(uri, 'access_token' => venmotoken, 'note' => note, 'user_id' => user,'amount' => amount, 'audience' => 'private' )
				puts res.body
			end

			@client = Twilio::REST::Client.new account_sid, auth_token
			message = @client.account.messages.create(:body => "auto_rent woke up and sent some venmo charges!",
			    :to => "+1234567890",
			    :from => "+1234567890")
			puts "Text sent with SID: #{message.sid}"
		else
	 		puts "auto_rent ran but it was not the day_to_bill"
		end
	rescue Exception=>e
		message = @client.account.messages.create(:body => "auto_rent failed terribly #{e.message}",
			    :to => "+1234567890",
			    :from => "+1234567890")
	end
end
