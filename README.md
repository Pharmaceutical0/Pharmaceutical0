from telethon.sync import TelegramClient

# Replace with your own values
api_id = '22464672'
api_hash = 'a2b288274c99d0077624e63a6a3e3422'
phone_number = '+601117181434'

# List of channel usernames to rank
channel_usernames = ['@andreybogdanov', '@andreybogdanov', '@andreybogdanov']

def get_channel_info(client, username):
    try:
        channel = client.get_entity(username)
        return {
            'username': username,
            'title': channel.title,
            'subscribers': channel.participants_count
        }
    except Exception as e:
        print(f"Failed to get info for {username}: {e}")
        return None

def main():
    with TelegramClient(phone_number, api_id, api_hash) as client:
        channel_data = []
        for username in channel_usernames:
            info = get_channel_info(client, username)
            if info:
                channel_data.append(info)
        
        # Sort channels by number of subscribers
        sorted_channels = sorted(channel_data, key=lambda x: x['subscribers'], reverse=True)
        
        # Print ranked channels
        for rank, channel in enumerate(sorted_channels, start=1):
            print(f"{rank}. {channel['title']} (@{channel['username']}) - Subscribers: {channel['subscribers']}")

if name == "__main__":
    main()
