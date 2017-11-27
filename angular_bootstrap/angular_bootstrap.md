% Διαδικτυακές και Νεφοϋπολογιστικές Εφαρμογές
% Αν. Καθηγητής Π. Λουρίδας
% Οικονομικό Πανεπιστήμιο Αθηνών

# Angular Boostrap

## Γενικά

* Είναι επίπονο να πετύχουμε ένα καλό αισθητικό αποτέλεσμα γράφοντας
  αρχεία CSS με το χέρι από το μηδέν.
  
* Η κατάσταση περιπλέκεται όταν πρέπει να λάβουμε υπόψη μας ότι η
  εφαρμογή μας θα πρέπει να εμφανίζεται σωστά σε διάφορες αναλύσεις
  και σε διαφορετικές συσκευές.
  
* Για το λόγο αυτό καλό είναι να χρησιμοποιούμε μια ώριμη βιβλιοθήκη
  στυλ.
  
* Μια τέτοια είναι το [Bootstrap](https://getbootstrap.com/).


# Εγκατάσταση

## Bootstrap και Angular

* Βεβαίως μπορούμε να χρησιμοποιήσουμε το Bootstrap ως έχει με το
  Angular, και στον κώδικά μας να χειριζόμαστε απευθείας τις κλάσεις
  στυλ και την JavaScript που προσφέρει.

* Είναι όμως απλούστερο να χρησιμοποιήσουμε μια βιβλιοθήκη η οποία μας
  δίνει πρόσβαση στο Boostrap μέσω των κατάλληλων εξαρτημάτων.

* Θα χρησιμοποιήσουμε τη βιβλιοθήκη
  [ng-bootstrap](https://ng-bootstrap.github.io/#/home). 

## Εγκατάσταση `ng-bootstrap`

* Εκτελούμε:

    ```bash
    npm install --save @ng-bootstrap/ng-bootstrap
    ```

* Στη συνέχεια θα πρέπει να ενημερώσουμε την εφαρμογή μας να
  χρησιμοποιεί τα στυλ του Bootstrap. 
  
* Στο αρχείο `index.html` προσθέτουμε στο στοιχείο `<head>` τη γραμμή:
  ```html
    <link rel="stylesheet"
        href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css"
        integrity="sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb"
        crossorigin="anonymous">
  ```

* Μετά χρειάζεται απλώς να εισάγουμε το ng-bootstrap στο
  `AppModule`.
  
* Προσθέτουμε κοντά στην αρχή του `app.module.ts`:
  ```javascript
  import {NgbModule} from '@ng-bootstrap/ng-bootstrap';
  ```
  
* Επίσης προσθέτουμε στον πίνακα `imports` τη γραμμή:
  ```javascript
  NgbModule.forRoot(),
  ```

## Καθάρισμα CSS

* Θα σταματήσουμε να χρησιμοποιούμε τα στυλ που είχαμε ορίσει μέχρι
  τώρα.
  
* Ξεκινάμε καθαρίζοντας το αρχείο `src/styles.css`

* Το ανοίγουμε και σβήνουμε όλα τα περιεχόμενά του, αφήνοντάς το κενό.


# Χρήση μπάρας πλοήγησης

## Πλοήγηση στην εφαρμογή

* Η εφαρμογή μας χρησιμοποιεί για πλοήγηση συνδέσμους στο πάνω μέρος
  της.

* Θα ενσωματώσουμε τη λογική των συνδέσμων στο Boostrap
  χρησιμοποιώντας μια μπάρα πλοήγησης.


## `app.module.html`

* Ανοίγουμε το `src/app/app.component.html` και το αλλάζουμε ως εξής:
  ```html
  <div class="container">
    <h1>{{title}}</h1>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <button class="navbar-toggler"
              type="button"
              data-toggle="collapse"
              data-target="#navbarSupportedContent"
              aria-controls="navbarSupportedContent"
              aria-expanded="false"
              aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item" routerLinkActive="active">
            <a class="nav-link"
               routerLink="/dashboard"
               href="#">Dashboard
              <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item" routerLinkActive="active">
            <a class="nav-link"
               routerLink="/books"
               href="#">Books</a>
          </li>
        </ul>
      </div>
    </nav>

    <router-outlet></router-outlet>
    <app-messages></app-messages>
  </div>
  ```

## `app.component.css`

* Ανοίγουμε το αρχείο `app.component.css` και το αδειάζουμε.


# Βελτίωση ταμπλό

## Χρήση Bootstrap στο ταμπλό

* Η εμφάνιση του ταμπλό ρυθμίζεται αυτή τη στιγμή από ένα περίπλοκο
  φύλλο στυλ.

* Αντί γι' αυτό, θα βασιστούμε στις δυνατότητες του Bootstrap.


## `dashboard.component.html` (1)

* Στο `dashboard.component.html` θα χρησιμοποιήσουμε ένα grid με
  τέσσερεις στήλες.

* Τα (μέχρι τέσσερα) βιβλία που θα εμφανίζονται θα μπαίνουν όλα μαζί
  σε μία σειρά που θα περιέχει τις στήλες αυτές.

## `dashboard.component.html` (2)

```html
<h3>Top Books</h3>
<div class="container">
  <div class="row">
    <a *ngFor="let book of books" class="col-sm"
       routerLink="/book/{{book.id}}">
      <div class="dashboard-item">
        <h5>{{book.title}}</h5>
      </div>
    </a>
  </div>
</div>

<app-book-search></app-book-search>
```

## `dashboard.component.css` (1)

* Τώρα μπορούμε να απλοποιήσουμε το `dashboard.css`.

* Στην ουσία θα κρατήσουμε μόνο ορισμένα στυλ, που αφορούν την
  επιμέρους προσαρμογή της εμφάνισης.


## `dashboard.component.css` (2)

```css
a {
  text-decoration: none;
}

h3 {
  text-align: center; margin-bottom: 1em;
}

h4 {
  position: relative;
}

.dashboard-item {
  padding: 20px;
  text-align: center;
  color: #eee;
  max-height: 120px;
  min-width: 120px;
  background-color: #607D8B;
  border-radius: 2px;
}

.dashboard-item:hover {
  background-color: #EEE;
  cursor: pointer;
  color: #607d8b;
}
```

# Βελτίωση αναζήτησης βιβλίων 

## Αναζήτηση μέσω typeahead

* Θα προσαρμόσουμε την αναζήτηση των βιβλίων που βρίσκεται κάτω από τα
  βιβλία στο dashboard.

* Αντί γι' αυτό, θα βασιστούμε στις δυνατότητες του Bootstrap, και
  συγκεκριμένα το widget typeahead.


## `book-search.component.html` (1)

* To `book-search.component.html` θα πρέπει να τροποποιηθεί όπως παρακάτω:
  ```html
  <div id="search-component">

    <ng-template #rt let-r="result">
      {{r.title}}
    </ng-template>

    <label for="search-box">Book search:</label>
    <input id="search-box"
           type="text"
           class="form-control"
           [class.is-invalid]="searchFailed"
           (selectItem)="selectedItem($event)"
           [(ngModel)]="model"
           [ngbTypeahead]="search"
           [resultTemplate]="rt"
           [inputFormatter]="formatter"/>

    <span *ngIf="searching">searching...</span>
    <div class="invalid-feedback" *ngIf="searchFailed">
      Sorry, suggestions could not be loaded.
    </div>
  </div> 
  ```

## `book-search.component.ts` (1)

* Αντίστοιχα θα πρέπει να τροποποιήσουμε το `book-search.component.ts`:
  ```javascript
  import { Component } from '@angular/core';
  import { Router } from '@angular/router';

  import { Observable } from 'rxjs/Observable';

  import 'rxjs/add/observable/of';
  import 'rxjs/add/operator/catch';
  import 'rxjs/add/operator/debounceTime';
  import 'rxjs/add/operator/distinctUntilChanged';
  import 'rxjs/add/operator/do';
  import 'rxjs/add/operator/map';
  import 'rxjs/add/operator/switchMap';
  import 'rxjs/add/operator/merge';

  import { Book } from '../book';
  import { BookService } from '../book.service';

  @Component({
    selector: 'app-book-search',
    templateUrl: './book-search.component.html',
    styleUrls: [ './book-search.component.css' ]
  })
  export class BookSearchComponent {
    public model: any;
    searching = false;
    searchFailed = false;
    hideSearchingWhenUnsubscribed =
      new Observable(() => () => this.searching = false);

    public books$: Observable<Book[]>;

    constructor(
      private router: Router,
      private bookService: BookService
    ) { }

    search = (text$: Observable<string>) =>
      text$
        .debounceTime(300)
        .distinctUntilChanged()
        .do(() => this.searching = true)
        .switchMap(term =>
          this.bookService.searchBooks(term)
            .do(() => this.searchFailed = false)
            .catch(() => {
              console.log('Failed!');
              this.searchFailed = true;
              return Observable.of([]);
            }))
        .do(() => {this.searching = false;} )
        .merge(this.hideSearchingWhenUnsubscribed);


    formatter = (b: Book) => b.title;

    selectedItem(item) {
      var book = item.item;
      this.router.navigate([`/book/${book.id}`]);
    }

  }
  ```


## `book-search.component.css`

* Τέλος, δεν χρειαζόμαστε κανένα από τα στυλ που είχαμε ορίσει για το
  `BookSearchComponent`, οπότε αλλάζουμε το αρχείο
  `book-search.component.css` ώστε να είναι:
  ```css
  .search-component {
    margin-top: 1em;
  }

  #search-box {
    width: 20em;
  }
  ```


# Προσθήκη κριτικών

## Επιστροφή στα μοντέλα

* Θέλουμε να προσθέσουμε τη δυνατότητα να βλέπουμε και να προσθέσουμε
  κριτικές στην εφαρμογή μας.
  
* Για να το κάνουμε αυτό, πρέπει να ξεκινήσουμε από τη back-end
  εφαρμογή που έχουμε γράψει στο Django.
  
  
## `models.py`

* Ας θυμηθούμε το αρχείο `models.py` το οποίο περιέχει τα μοντέλα μας:

```python
from django.db import models
from django.utils import timezone

class Book(models.Model):
    title = models.CharField(max_length=200)
    pub_year = models.IntegerField('date published', default=2000)

    def was_published_recently(self):
        return (self.pub_year >= timezone.now().year - 1)
    
    def __str__(self):
        return "%s %s" % (self.title, self.pub_year)
    
class Review(models.Model):
    book = models.ForeignKey(Book, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    text = models.TextField(default="")
    review_date = models.DateTimeField('review date',
                                       default=timezone.now)

    def __str__(self):
        return "%s %s %s" % (self.title, self.text, self.review_date)

class Author(models.Model):
    name = models.CharField(max_length=200)
    books = models.ManyToManyField(Book)

    def __str__(self):
        return self.name

```

## `serializers.py`

* Θα πρέπει να προσθέσουμε τον κατάλληλο serializer για τις κριτικές
  των βιβλίων:

```python
from rest_framework import serializers
from .models import Book, Review

class BookSerializer(serializers.ModelSerializer):
    class Meta:
        model = Book
        fields = ('id', 'title', 'pub_year')

class ReviewSerializer(serializers.ModelSerializer):
    class Meta:
        model = Review
        fields = ('id', 'title', 'text', 'review_date', 'book')
```


## `views.py`

* Αντίστοιχα, θα προσθέσουμε δύο νέα views, μία για να παίρνουμε όλες
  τις κριτικές, και μία για να μπορούμε να χειριστούμε μία.

```python
from .models import Book, Review
from .serializers import BookSerializer, ReviewSerializer
from rest_framework import generics

from django.contrib.staticfiles import views

def index(request, path=''):
    if (path.endswith('.js')):
        return views.serve(request, path)
    else:
        return views.serve(request, 'index.html')

class BookList(generics.ListCreateAPIView):
    serializer_class = BookSerializer

    def get_queryset(self):
        queryset = Book.objects.all()
        title = self.request.query_params.get('title', None)
        if title is not None:
            queryset = queryset.filter(title__contains=title)
        return queryset

class BookDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Book.objects.all()
    serializer_class = BookSerializer

class ReviewList(generics.ListCreateAPIView):
    queryset = Review.objects.all().order_by('-review_date')
    serializer_class = ReviewSerializer

class ReviewDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Review.objects.all()
    serializer_class = ReviewSerializer
```


## Επέκταση του API

* Οι κριτικές, μιας και αναφέρονται πάντοτε σε ένα βιβλίο, θα είναι
  προσπελάσιμες μέσω αυτού.
  
* Έτσι, για να δούμε τις κριτικές ενός βιβλίο, θα δίνουμε:
  ```
  GET /api/books/book_id/reviews
  ```

* Για να δημιουργήσουμε μια κριτική, θα δίνουμε:
  ```
  PUT /api/books/book_id/reviews/
  ```

* Ενώ για να αλλάξουμε μια κριτική, θα δίνουμε:
  ```
  PUT /api/books/book_id/reviews/review_id
  ```

## `djbr/urls.py`

* Για να επιτύχουμε τα παραπάνω, αλλάζουμε το αρχείο `djbr/urls.py`
  ώστε να είναι:

```python
from django.conf.urls import url
from . import views

app_name = 'djbr'

urlpatterns = [
    url(r'^books/?$', views.BookList.as_view()),
    url(r'^books/(?P<pk>[0-9]+)/?$', views.BookDetail.as_view()),
    url(r'^books/(?P<pk>[0-9]+)/reviews/?$', views.ReviewList.as_view()),
]
```

## Επιστροφή στο front-end

* Στο front-end τώρα, θα πρέπει να επεκτείνουμε την εφαρμογή του
  Angular ώστε να μπορεί να εμφανίσει και να χειριστεί κριτικές.
  
* Θα λειτουργήσουμε περίπου όπως και στα βιβλία.


## Δημιουργία κλάσης `Review`

* Δημιουργούμε μια κλάση `Review`, η οποία θα αποτελέσει το μοντέλο
  μας στο front-end:
  ```bash
  ng generate class review
  ```

* Θα δούμε ότι δημιουργήθηκε το αρχείο:
  ```
  src/app/review.ts
  ```

## `review.ts`

* Αλλάζουμε το αρχείο `review.ts` ώστε να περιέχει τα παρακάτω:
  ```javascript
  export class Review {
    id: number;
    book: number;
    title: string;
    text: string;
  }
  ```

## Δημιουργία `ReviewsComponent`

* Για την εμφάνιση και το χειρισμό των κριτικών θα δημιουργήσουμε ένα
  εξάρτημα `ReviewsComponent`.
  
* Δίνουμε:
  ```bash
  ng generate component reviews
  ```
  
* Θα δημιουργηθούν τα αρχεία:
  * `reviews.component.css`
  * `reviews.component.html`
  * `reviews.component.spec.ts`
  * `reviews.component.ts`
  
* Επίσης, θα ενημερωθεί κατάλληλα το αρχείο `app.module.ts`.


## Δημιουργία `ReviewService`

* Για την επικοινωνία με το back-end όσον αφορά τις κριτικές, θα
χρησιμοποιήσουμε μία υπηρεσία `ReviewService`.

* Δίνουμε:
  ```bash
  ng generate service review
  ```
  
* Θα δημιουργηθούν τα αρχεία:
  * `review.service.spec.ts`
  *  `review.service.ts`

## Ενημέρωση `app.module.ts`

* Θα πρέπει να ενημερώσουμε το αρχείο `app.module.ts` για την υπηρεσία
  που φτιάξαμε.
  
* Θα πρέπει να την εισάγουμε:
  ```javascript
  import { ReviewService } from './review.service';
  ```
  
* Θα πρέπει να την προσθέσουμε στους `providers`:
  ```javascript
  providers: [ BookService, MessageService, ReviewService ],
  ```

## Ενημέρωση διαδρομών

```javascript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

import { BooksComponent } from './books/books.component';
import { BookDetailComponent } from './book-detail/book-detail.component';
import { DashboardComponent } from './dashboard/dashboard.component';
import { ReviewsComponent } from './reviews/reviews.component';

const routes: Routes = [
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' },
  { path: 'books', component: BooksComponent },
  { path: 'dashboard', component: DashboardComponent },
  { path: 'books/:id', component: BookDetailComponent },
  { path: 'books/:id/reviews', component: ReviewsComponent },
];

@NgModule({
  imports: [ RouterModule.forRoot(routes) ],
  exports: [ RouterModule ]
})
export class AppRoutingModule { }
```

## `reviews.component.html`

```html
<div class="container">
  <h3>Reviews</h3>

  <form (ngSubmit)="onSubmit()" #reviewForm="ngForm">
    <div class="form-group">
      <label for="title">Title</label>
      <input type="text"
             class="form-control"
             id="title"
             [(ngModel)]="review.title"
             name="title"
             required>
    </div>

    <div class="form-group">
      <label for="text">Content</label>
      <input type="text"
             class="form-control"
             id="text"
             [(ngModel)]="review.text"
             name="text">
    </div>

    <button type="submit" class="btn btn-success">Submit</button>

  </form>

  <ul>
    <li *ngFor="let review of reviews">
      {{ review.title }}
      {{ review.text }}
    </li>
  </ul>
</div>
```

## `reviews.component.ts`

```javascript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute, ParamMap } from '@angular/router';

import 'rxjs/add/operator/switchMap';
import 'rxjs/add/operator/do';

import { Review } from '../review';
import { ReviewService } from '../review.service';

@Component({
  selector: 'app-reviews',
  templateUrl: './reviews.component.html',
  styleUrls: ['./reviews.component.css'],
})
export class ReviewsComponent implements OnInit {

  reviews: Review[];

  review: Review;

  constructor(
    private route: ActivatedRoute,
    private reviewService: ReviewService
  ) {
    this.review = this.newReview();
  }

  ngOnInit() {
    this.route.paramMap
      .switchMap((params: ParamMap) => {
        let bookId = +params.get('id');
        this.review = this.newReview();
        this.review.book = bookId;
        return this.reviewService.getReviews(+params.get('id'))
      }).subscribe(reviews => this.reviews = reviews);
  }

  newReview() : Review {
    var review = new Review();
    review.title = '';
    review.text = '';
    return review;
  }

  onSubmit() : void {
    console.log(this.review);
    this.reviewService.addReview(this.review)
      .subscribe(review => this.reviews.unshift(review));
  }

}

```

## Χρήση του `switchMap`

* Ενδέχεται ο χρήστης να πλοηγηθεί στη σελίδα με τις κριτικές ενός
  συγκεκριμένου βιβλίου (με συγκεκριμένο `id`) ενώ ήδη αναζητούμε τις
  κριτικές ενός προηγούμενου βιβλίου (με άλλο `id`).
  
* Ο τελεστής `switchMap` εξασφαλίζει ότι δεν θα ληφθούν υπόψη τα αποτελέσματα
  της προηγούμενης αίτησης `getReviews()`, αλλά μόνο της τρέχουσας.
  

## `review.service.ts`

```javascript
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';

import { Observable } from 'rxjs/Observable';
import { of } from 'rxjs/observable/of';
import { catchError, map, tap } from 'rxjs/operators';

import { MessageService } from './message.service';

import { Review } from './review';

const httpOptions = {
  headers: new HttpHeaders({ 'Content-Type': 'application/json' })
};

@Injectable()
export class ReviewService {

  constructor(
    private http: HttpClient,
    private messageService: MessageService
  ) { }

  /** GET reviews from the server */
  getReviews(bookId: number): Observable<Review[]> {
    let url = `api/books/${bookId}/reviews`;
    return this.http.get<Review[]>(url)
      .pipe(
        tap(reviews => this.log(`fetched reviews`)),
        catchError(this.handleError('getReviews', []))
      );
  }

  /** POST: add a new review to the server */
  addReview(review: Review): Observable<Review> {
    let url = `api/books/${review.book}/reviews`;
    return this.http.post<Review>(url, review, httpOptions).pipe(
      tap((review: Review) => this.log(`added review w/ id=${review.id}`)),
      catchError(this.handleError<Review>('addReview'))
    );
  }

  /**
   * Handle Http operation that failed.
   * Let the app continue.
   * @param operation - name of the operation that failed
   * @param result - optional value to return as the observable result
   */
  private handleError<T> (operation = 'operation', result?: T) {
    return (error: any): Observable<T> => {

      console.error(error); // log to console instead

      this.log(`${operation} failed: ${error.message}`);

      // Let the app keep running by returning an empty result.
      return of(result as T);
    };
  }

  private log(message: string): void {
    this.messageService.add('ReviewService: ' + message);
  }

}
```


## `books.component.html`

* Τέλος, θέλουμε το εξάρτημα των κριτικών να εμφανίζεται στη σελίδα με
  τις λεπτομέρειες ενός βιβλίου:
  ```html
  <div *ngIf="book">
    <h2><span appItalics> {{ book.title }}</span> details:</h2>
    <div><label>id: </label>{{book.id}}</div>
    <div>
      <label>title: </label>
      <input [(ngModel)]="book.title" placeholder="name">
    </div>
    <div><label>Publication year: </label>{{book.pub_year}}</div>
    <button (click)="goBack()">go back</button>
    <button (click)="save()">Save</button>

    <app-reviews></app-reviews>
  </div>
  ```