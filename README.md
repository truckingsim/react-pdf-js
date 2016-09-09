#react-pdf-js-worker
---
[![NPM Version](https://img.shields.io/npm/v/react-pdf-js-worker.svg?style=flat-square)](https://www.npmjs.com/package/react-pdf-js-worker)
[![NPM Downloads](https://img.shields.io/npm/dm/react-pdf-js-worker.svg?style=flat-square)](https://www.npmjs.com/package/react-pdf-js-worker)
[![Build Status](https://img.shields.io/travis/truckingsim/react-pdf-js-worker/master.svg?style=flat-square)](https://travis-ci.org/truckingsim/react-pdf-js-worker)
[![dependencies Status](https://david-dm.org/truckingsim/react-pdf-js-worker/status.svg)](https://david-dm.org/truckingsim/react-pdf-js-worker)
[![devDependencies Status](https://david-dm.org/truckingsim/react-pdf-js-worker/dev-status.svg)](https://david-dm.org/truckingsim/react-pdf-js-worker?type=dev)

`react-pdf-js-worker` provides a component for rendering PDF documents using [PDF.js](http://mozilla.github.io/pdf.js/). Written for React 15 and ES2015 using the Airbnb style guide.

---

Usage
-----

Install with `npm install react-pdf-js-worker`

Use in your app (showing some basic pagination as well):

```js
import React from 'react';
import PDF from 'react-pdf-js-worker';

class MyPdfViewer extends React.Component {
  constructor(props) {
    super(props);
    this.onDocumentComplete = this.onDocumentComplete.bind(this);
    this.onPageCompleted = this.onPageCompleted.bind(this);
    this.handlePrevious = this.handlePrevious.bind(this);
    this.handleNext = this.handleNext.bind(this);
  }

  onDocumentComplete(pages) {
    this.setState({ page: 1, pages });
  }

  onPageCompleted(page) {
    this.setState({ page });
  }

  handlePrevious() {
    this.setState({ page: this.state.page - 1 });
  }

  handleNext() {
    this.setState({ page: this.state.page + 1 });
  }

  renderPagination(page, pages) {
    let previousButton = <li className="previous" onClick={this.handlePrevious}><a href="#"><i className="fa fa-arrow-left"></i> Previous</a></li>;
    if (page === 1) {
      previousButton = <li className="previous disabled"><a href="#"><i className="fa fa-arrow-left"></i> Previous</a></li>;
    }
    let nextButton = <li className="next" onClick={this.handleNext}><a href="#">Next <i className="fa fa-arrow-right"></i></a></li>;
    if (page === pages) {
      nextButton = <li className="next disabled"><a href="#">Next <i className="fa fa-arrow-right"></i></a></li>;
    }
    return (
      <nav>
        <ul className="pager">
          {previousButton}
          {nextButton}
        </ul>
      </nav>
      );
  }

  render() {
    let pagination = null;
    if (this.state.pages) {
      pagination = this.renderPagination(this.state.page, this.state.pages);
    }
    return (
      <div>
        <PDF file="somefile.pdf" onDocumentComplete={this.onDocumentComplete} onPageCompleted={this.onPageCompleted} page={this.state.page} />
        {pagination}
      </div>
  }
}

module.exports = MyPdfViewer;
```


## Credit

This project is a fork of [react-pdf-js](https://github.com/mikecousins/react-pdf-js) which is a fork of [react-pdfjs](https://github.com/erikras/react-pdfjs) which itself was a port of [react-pdf](https://github.com/nnarhinen/react-pdf), so thank you to
the original authours.
