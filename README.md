## 1. Book Component with Service

### book.service.ts
```ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class BookService {
  private books = [
    { id: 1, name: 'The Alchemist' },
    { id: 2, name: 'Rich Dad Poor Dad' },
    { id: 3, name: 'Atomic Habits' }
  ];

  getBooks() {
    return this.books;
  }
}
```

### book.component.ts
```ts
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { BookService } from '../book.service';

@Component({
  selector: 'app-book',
  standalone: true,
  templateUrl: './book.component.html',
  styleUrls: ['./book.component.css'],
  imports: [CommonModule]
})
export class BookComponent {
  books:{id:number, name:string}[] = [];
  constructor(private bookService: BookService) {
    this.books = this.bookService.getBooks();
  }
}
```

### book.component.html
```html
<h2>Book List</h2>
<ul>
  <li *ngFor="let book of books">{{ book.id }} - {{ book.name }}</li>
</ul>
```

### app.component.html
```html
<app-book></app-book>
```

### app.component.ts
```ts
import { Component } from '@angular/core';
import { BookComponent } from './book/book.component';

@Component({
  selector: 'app-root',
  imports: [BookComponent],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  title = 'demo';
}
```

---

## 2. Order Status with ngSwitch

### app.component.ts
```ts
import { CommonModule } from '@angular/common';
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  status: string = 'shipped';
}
```

### app.component.html
```html
<h2>Order Status</h2>

<div [ngSwitch]="status">
  <p *ngSwitchCase="'pending'">🟡 Your order is pending.</p>
  <p *ngSwitchCase="'shipped'">🚚 Your order has been shipped.</p>
  <p *ngSwitchCase="'delivered'">✅ Your order has been delivered.</p>
  <p *ngSwitchDefault>❌ Invalid status.</p>
</div>
```

---

## 1. Form Component

**app.component.html**
```html
<h2>Course Registration</h2>

<form #courseForm="ngForm" (ngSubmit)="onSubmit(courseForm)">
  <div>
    <label>Name:</label>
    <input type="text" name="name" [(ngModel)]="course.name" required />
  </div>

  <div>
    <label>Email:</label>
    <input type="email" name="email" [(ngModel)]="course.email" required />
  </div>

  <div>
    <label>Course:</label>
    <input type="text" name="course" [(ngModel)]="course.course" required />
  </div>

  <button type="submit" [disabled]="!courseForm.valid">Register</button>
</form>
```

**app.component.ts**
```ts
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';
@Component({
  selector: 'app-root',
  imports: [FormsModule],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  course = {
    name: '',
    email: '',
    course: ''
  };

  onSubmit(form: any) {
    console.log('Form submitted:', form.value);
    alert('Course Registered Successfully!');
  }
}
```

---
