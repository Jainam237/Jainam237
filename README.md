from flask import Flask, render_template, request, session, redirect, url_for

app = Flask(__name__)
app.secret_key = 'your_secret_key'


@app.route('/')
def index():
    return render_template('index.html')


@app.route('/add_to_cart/<item>')
def add_to_cart(item):
    if 'cart' not in session:
        session['cart'] = []

    session['cart'].append(item)
    return redirect(url_for('index'))


@app.route('/view_cart')
def view_cart():
    cart_items = session.get('cart', [])
    return render_template('cart.html', cart_items=cart_items)


if __name__ == '__main__':
    app.run(debug=True)
