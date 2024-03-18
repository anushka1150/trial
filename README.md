from flask import Flask, request, jsonify

app = Flask(__name__)

def filter_arrays(input_array):
    evens = [num for num in input_array if num % 2 == 0 and isinstance(num, int)]
    odds = [num for num in input_array if num % 2 != 0 and isinstance(num, int)]
    alphabets = [char.upper() for char in input_array if isinstance(char, str) and char.isalpha()]
    return evens, odds, alphabets

@app.route('/process_array', methods=['POST'])
def process_array():
    data = request.json
    if 'array' not in data or not isinstance(data['array'], list):
        return jsonify({'error': 'Invalid input'}), 400
   
    input_array = data['array']
    evens, odds, alphabets = filter_arrays(input_array)
   
    response = {
        'is_success': True,
        'user_id': '123',  # Example user ID
        'roll_number': '456',  # Example college roll number
        'email': 'example@example.com',  # Example email
        'even_numbers': evens,
        'odd_numbers': odds,
        'alphabets_uppercase': alphabets
    }
   
    return jsonify(response)

if __name__ == '__main__':
    app.run(debug=True)

