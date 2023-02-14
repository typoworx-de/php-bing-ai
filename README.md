# Bing AI

## Install

    composer require maximerenou/bing-ai

## Usage

Edit and run `examples/chat.php` to test it.

```php
use MaximeRenou\BingAI\BingAI;
use MaximeRenou\BingAI\Chat\Prompt;

// $cookie - your "_U" cookie from bing.com
$ai = new BingAI;
$conversation = $ai->createChatConversation($cookie)
    ->withLocation($latitude, $longitude, $radius) // Optional
    ->withPreferences('fr-FR', 'fr-FR', 'FR'); // Optional

// Example 1: sync
// $text - Text-only version of Bing's answer
// $messages - Message objects array
list($text, $messages) = $conversation->ask(new Prompt("Hello World"));

// Example 2: async
// $text - Incomplete text version
// $messages - Incomplete messages fleet
list($final_text, $final_messages) = $conversation->ask($prompt, function ($text, $cards) {
    echo $text;
});

```

If you want to resume a previous conversation, you can retrieve its identifiers:
```php
// Get current identifiers
$identifiers = $conversation->getIdentifiers();

// ...
// Resume conversation with $identifiers parameter
$conversation = $ai->createChatConversation($cookie, $identifiers);
```