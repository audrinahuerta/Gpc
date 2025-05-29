inventory = {
    'product1': {'name': 'Awesome T-Shirt', 'quantity': 50, 'price': 20.00},
    'product2': {'name': 'Cool Mug', 'quantity': 100, 'price': 10.00}
}

@app.route('/inventory', methods=['GET'])
def get_inventory():
    return jsonify(inventory)

@app.route('/inventory/<product_id>', methods=['GET'])
def get_product(product_id):
    if product_id in inventory:
        return jsonify(inventory[product_id])
    return jsonify({'message': 'Product not found'}), 404

@app.route('/inventory/<product_id>/update', methods=['POST'])
def update_inventory(product_id):
    if product_id in inventory:
        data = request.get_json()
        inventory[product_id]['quantity'] = data['quantity']
        return jsonify({'message': 'Inventory updated'})
    return jsonify({'message': 'Product not found'}), 404

if __name__ == '__main__':
    app.run(debug=True)
```
